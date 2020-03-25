---
title: Notas de versão anteriores do AEM 6.5 Service Pack
description: Notas de versão específicas do Adobe Experience Manager 6.5 Service Pack 3 e anterior.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: 0e95ac8850a693764b82a29960b472d156dac535

---


# Correções e Feature Packs incluídos em Pacotes de serviço anteriores {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## Adobe Experience Manager 6.5.3.0

[!DNL Adobe Experience Manager] 6.5.3.0 é uma versão importante que inclui correções e melhorias de desempenho, estabilidade, segurança e essenciais para o cliente lançadas desde a disponibilização geral da versão 6.5 em **abril de 2019**. It can be installed on top of [!DNL Adobe Experience Manager] 6.5.

Alguns destaques principais desta versão do Service pack:

* O repositório integrado (Apache Jackrabbit Oak) foi atualizado para a versão 1.10.6.

* [!DNL Experience Manager Assets] agora suporta arquivos ZIP criados com o algoritmo Deflate64.

* A nova coluna para a data criada, que é classificável, foi adicionada na visualização de lista DAM e nos resultados da pesquisa de ativos na visualização de listas.

* A classificação de ativos com base na coluna Nome foi ativada na visualização de Lista.

* [!DNL Dynamic Media] agora é compatível com ativos de vídeo de Recorte inteligente. O Smart Crop é um recurso orientado por aprendizado de máquina que recorta um vídeo enquanto move o quadro para seguir o ponto focal da cena.

* [!DNL Dynamic Media] suporta a criação de imagens inteligentes.

* Capacidade de [definir preferências de Ausência Temporária](../forms/using/configure-out-of-office-settings.md) em [!DNL Experience Manager] workflows.

* Capacidade de [compartilhar itens](../forms/using/configure-shared-queues-osgi.md) de Caixa de entrada ou Caixa de entrada com outros usuários em [!DNL Experience Manager] workflows.

* Capacidade de [gerar Comunicações interativas no modo](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)Lote.

* Versão atualizada do jQuery fornecido no ContextHub para 3.4.1.

### Ativos {#assets-6530-enhancements}

**Aprimoramentos do produto**

* [!DNL Experience Manager Assets] agora suporta arquivos ZIP criados com o algoritmo Deflate64 (NPR-27573).

* A nova coluna para a data criada, que é classificável, foi adicionada na visualização de lista DAM e nos resultados da pesquisa de ativos na visualização de lista (NPR-31312).

* A classificação de ativos com base na coluna Nome foi permitida na visualização da Lista (NPR-31299).

* Os arquivos de ativos GLB, GLTF, OBJ e STL suportam a pré-visualização de ativos na página Detalhes do ativo no DAM (CQ-4282277).

* O evento ReplicationOnModifyListener é acionado para nós de segmentos durante o carregamento de segmentos em [!DNL Dynamic Media] (CQ-4281279).

* [!DNL Dynamic Media] agora é compatível com ativos de vídeo de Recorte inteligente. O Smart Crop é um recurso acionado pelo aprendizado de máquina que recorta um vídeo enquanto move o quadro para seguir o ponto focal da cena (CQ-4278995).

* [!DNL Dynamic Media] suporta Smart Imaging (CQ-4222249).

* A visualização de pesquisa/navegação foi definida como visualização padrão no seletor do Foundation se os parâmetros de query forem transmitidos na solicitação (NPR-31601).

**Correções**

* Os metadados de alguns documentos PDF não são atualizados e salvos no PDF ao modificar seu título (NPR-31629).

* O compartilhamento de ativos não funciona para ativos com o caractere &quot;+&quot; em seus nomes (NPR-31547).

* As edições no formulário de pesquisa padrão Assets Admin * Search Rail não funcionam como esperado (NPR-31502).

* As sugestões não são mostradas ao usar o Omnisearch em ativos visualização para pesquisar ativos (NPR-31496).

* As referências de ativos em coleções não são atualizadas quando os ativos referenciados são movidos para outro local, nos casos em que os mesmos ativos são referenciados por coleção diferente por usuários diferentes (NPR-31486).

* As tags IPTC do Duplicado são adicionadas aos metadados do ativo (NPR-31328).

* A contagem de resultados da pesquisa no canto superior direito não é atualizada corretamente quando a pesquisa é acionada do painel de filtros (NPR-31316).

* Todas as caixas de seleção são desmarcadas ao desmarcar as caixas de seleção de segundo nível no filtro Tipo de arquivo, e o texto na barra de pesquisa não está sincronizado com as propriedades selecionadas/não selecionadas (NPR-31287).

* Não é possível remover todos os membros (utilizadores/grupos) da seção Membros de uma pasta; ao tentar remover todos os usuários, o usuário conectado é adicionado à lista (NPR-31171).

* Os ativos com o símbolo &quot;+&quot; no nome do arquivo não podem ser excluídos (NPR-31162).

* O menu suspenso Criar, que está visível no menu superior ao selecionar uma pasta, não mostra a opção &quot;Pasta&quot; como uma opção de criação (NPR-30877).

* A seleção de pasta Criar > item de ação FileUpload está ausente quando a ACL para Negar jcr:removeChildNodes e jcr:removeNode no caminho é aplicada para um usuário (NPR-30840).

* workflows DAM entram em estado obsoleto quando determinados ativos mp4 são carregados, fazendo com que todos os workflows restantes entrem em estado obsoleto (NPR-30662).

* Erro de falta de memória é observado quando um grande arquivo PDF (de vários Gigabytes) é carregado no DAM e seus subativos são processados (NPR-30614).

* A movimentação em massa de ativos está falhando e exibindo a mensagem de aviso (NPR-30610).

* Os nomes dos ativos são alterados para minúsculas ao mover ativos de uma pasta para outra em [!DNL Experience Manager] execução no modo de execução [!DNL Dynamic Media] Scene 7 (NPR-31630).

* Ocorreu um erro ao editar um conjunto de imagens remoto, para a imagem que reside na pasta com o mesmo nome de empresa do Scene 7 (NPR-31340).

* [!DNL Dynamic Media] ativos que contêm referências não estão sendo publicados (NPR-31180).

* Os carregamentos de [!DNL Experience Manager Dynamic Media] - modo de execução Scene 7 para Scene 7 estão demorando muito para serem concluídos (NPR-31048).

* O ponto de acesso adicionado a um ativo de imagem não é visível por meio do Visualizador de imagem interativo na página de detalhes do ativo (NPR-30979).

* Grandes trabalhos de sling são criados e o banner Processamento é reexibido quando as ações realizadas em ativos [!DNL Experience manager Assets] são passadas para o Scene 7 (NPR-30947).

* O conflito ocorre ao criar a Cópia de idioma dos ativos e os ativos não são carregados para o Scene 7 (NPR-30932).

* As renderizações dinâmicas baixadas da [!DNL Experience Manager] execução no modo [!DNL Dynamic Media] Híbrido estão quebradas (elas são do tipo de texto com o conteúdo &quot;não é possível localizar a imagem&quot; em vez do tipo de conteúdo de imagem) (NPR-30876).

* [!DNL Dynamic Media] O fluxo de trabalho Codificar vídeo está falhando ao gerar miniatura para o vídeo que é migrado do modo de execução Scene 7 para [!DNL Dynamic Media] - Scene 7 (CQ-4282011).

* IpsApiException observou ao migrar ativos de uma instância para outra usando IDs de empresa Scene 7 diferentes (CQ-4280548).

* A miniatura de ativos 3D não é informativa quando um modelo 3D suportado é assimilado [!DNL Experience Manager] (CQ-4283701).

* Os botões de rolagem são exibidos no visualizador, se um ativo 3D tiver poucas visualizações de câmera (CQ-4283322).

* Altura incorreta do container de um modelo 3D carregado visualizado no DimensionalViewer na página Detalhes do ativo (CQ-4283309).

* Os vídeos não podem ser reproduzidos com o SmartCropVideoViewer no Internet Explorer 11 e no Safari (CQ-4281422).

* O uso do botão mover para mover vários ativos, de uma pasta para outra, falha ao [!DNL Experience Manager] executar em [!DNL Dynamic Media] - modo de execução cena7 (CQ-4280384).

* Vídeo distorcido é visto nos detalhes do ativo quando o tipo MIME é diferente de MP4 (CQ-4279704).

* Os vídeos recém-ingeridos em pastas com perfil de vídeo permanecem no estado de processamento mesmo após a porcentagem de codificação ser concluída para 100% (CQ-4279389).

* Mover ativos de uma pasta cria um grande número de tarefas de sling (chamadas de API Scene 7) do que o ideal (CQ-4278664).

* Os nomes do conjunto de imagens são alterados para minúsculas na Cena 7, quando o conjunto de imagens (ou conjunto de imagens) é criado e nomeado com a convenção de nomenclatura apropriada no DAM (CQ-4281112).

* O Scene 7 Migrator define o estado de publicação incorretamente (CQ-4263492).

* A página de resultados da pesquisa de interface de toque (feita pelo Omnisearch) rola automaticamente para cima e perde a posição de rolagem do usuário em Fragmentos de conteúdo (CQ-4282898).

* Os arquivos PDF não são indexados e o conteúdo não é pesquisável (CQ-4278916).

* Erro &quot;Grupo não listado pelo seletor de usuários: esperado &quot;falso para igual a verdadeiro&quot; é observado ao adicionar o Grupo de usuários fechado com diferentes `principalName` e `authorizableId` (CQ-4278177).

* A Visualização da coluna da interface do usuário do Assets está mostrando todos os caminhos, independentemente do caminho raiz do locatário específico (CQ-4278175).

* A pesquisa do seletor de ativos não está funcionando como esperado (CQ-4275886).

* Os Workflows de execução estão com falha (CQ-4271928).

* A Expurgação do Evento DAM exclui os dados mais recentes do evento (maxSavedActivities) e retém os dados criados anteriormente (NPR-31336).

* A página de resultados da pesquisa de interface de toque (feita pelo Omnisearch) rola automaticamente para cima e perde a posição de rolagem do usuário (NPR-31307).

* A barra de ações e a contagem de ativos não são atualizadas ao selecionar todos e depois desmarcar alguns itens (pastas/ativos individuais) na interface de usuário do toque (NPR-31118).

* Uma exceção é exibida durante [!DNL Experience Manager] a pesquisa para obter detalhes de um ativo (CQ-4283569).

### Sites {#sites}

* Se a herança do LiveCopy for quebrada, as páginas de Live Copy exibirão links de cópia de idioma em vez de links do LiveCopy (NPR-30980).
* Para um novo Blueprint, se o número de registros for superior a 40, somente os primeiros 40 registros serão exibidos. O Blueprint exibe linhas em branco para o restante dos registros (NPR-31182).
* Quando um usuário adiciona caracteres japoneses ou coreanos na propriedade de descrição de um menu, o menu exibe caracteres distorcidos para o texto em japonês e coreano. (NPR-31331).
* O Editor de Rich Text (RTE) não permite inserir uma Tabela incorporada como um item de lista (NPR-30879).
* Fora da caixa, andaime do Editor de Rich Text (RTE). aplica o tamanho da fonte embutida a elementos, inesperadamente (NPR-31284).
* Quando um usuário foca nos campos do painel à esquerda e usa um atalho do teclado para colar o conteúdo, ele cola o conteúdo da área de transferência do editor de páginas em vez do conteúdo copiado dos campos do painel à esquerda (NPR-31172).
* Quando um usuário adiciona um campo Upload de arquivo a um campo múltiplo, o caminho da imagem é armazenado no nó do componente em vez do nó de vários campos (NPR-30882).
* A API ResponsiveGridExporter não retorna a interface com.day.cq.wcm.Foundation.model.impl.export.AllowedComponentsExporter. O pacote com.day.cq.wcm.Foundation.model.impl é declarado como pacote privado (NPR-31398).
* Quando uma página que contém alguns Fragmentos de experiência é aberta no modo não editor (no Autor sem o `editor.html` prefixo e `wcmmode=disabled`, ou no Editor)., a solicitação termina no código de erro de status HTTP 500 (NPR-30743).
* Os usuários não podem alterar sua senha e acessar sua página do perfil (NPR-31161).

### Pesquisa e interface do usuário {#search-ui-interface}

* Ao alternar da visualização de cartão para a visualização de Lista em uma página de resultados de pesquisa, há um atraso antes que a página possa ser rolada (NPR-31286).

* A caixa de seleção Selecionar tudo está oculta na visualização de Lista na [!DNL Sites] interface do usuário (NPR-31614).

* A contagem Selecionar tudo em uma página de resultados de pesquisa está incorreta (NPR-31120).

* O editor de metadados exibe tags que não existem (NPR-31119).

### Tradução {#translation}

* Dois pop-ups de calendário são exibidos ao selecionar a opção Data de vencimento em um trabalho de tradução (NPR-31270).

### Plataforma {#platform}

* A opção de tipo Mime no console da Web não funciona (NPR-31108).

* O certificado do cliente não é aceito ao configurar o logon único (NPR-31165).

* As atualizações na configuração de tamanho do buffer do serviço HTTP baseado em Java não são salvas (NPR-30925).

* O QueryBuilder agora suporta orderby ``fn:name()`` em query xpath (NPR-31322).

* A árvore de ativação do Duplicado é criada ao atualizar da versão [!DNL Experience Manager] 6.3 (NPR-31513).

* As solicitações encaminhadas não preservam cabeçalhos de resposta que são definidos durante a autenticação Sling (NPR-30013).

* A pesquisa nos componentes do seletor não funciona (NPR-31692).

* Um erro é exibido ao anexar um arquivo ZIP a uma [!DNL Experience Manager Communities] publicação devido a diferentes versões do pacote Apache POI e Apache Tika (NPR-31018).

* O ``org.apache.sling.distribution.api`` pacote está oculto no gerenciador de configuração e, portanto, não está disponível para pacotes personalizados (NPR-31720).

### Projetos {#projects}

* A alternância de visualizações de calendário não funciona (NPR-31271).

### Brand Portal {#assets-brand-portal}

**Aprimoramentos do produto**

* O fluxo de trabalho de importação da Origem de ativos no [!DNL Experience Manager Assets] é modificado para buscar apenas os ativos recém-criados de [!DNL Brand Portal] para [!DNL Experience Manager]e ignorar os ativos que já existem na pasta NEW para evitar a replicação (CQ-4278527).

**Correções**

* O ícone incorreto é exibido ao criar uma nova pasta Contribuição no recurso Origem de ativos (CQ-4282825).
* Ao criar uma nova pasta de contribuição, uma ou ambas as subpastas (NOVO e COMPARTILHADO) não aparecem na pasta de contribuição (CQ-4282424).
* O sistema lança uma exceção se o usuário tentar republicar a pasta Contribuição de [!DNL Experience Manager] para [!DNL Brand Portal] depois de receber novos ativos na pasta Contribuição do [!DNL Brand Portal] fim (CQ-4279740).
* A criação da pasta Contribuição em uma pasta Contribuição (pasta aninhada) é proibida para evitar a complexidade (CQ-4278391).
* O sistema lança uma exceção ao fazer upload da lista do [!DNL Brand Portal] usuário (arquivo .csv) importada do [!DNL Experience Manager] Admin Console. Somente os campos Email, Nome e Sobrenome no arquivo .csv são obrigatórios (CQ-4278390).

### Communities {#communities}

**Correções**

* Os links rápidos para gerenciar grupos (Abrir/Editar/Publicar/Excluir grupos) não estão visíveis para os administradores da Comunidade (Administrador de grupo/Administrador de site) (NPR-31627).
* Um blog enviado não é exibido, a menos que a página seja atualizada/recarregada manualmente (NPR-31599).
* O query JCR usado pelo recurso &quot;Menções&quot; diferencia maiúsculas de minúsculas e demora muito para retornar os resultados (NPR-31475).
* [!DNL Experience Manager] 6.5 O arquivo UberJar lança uma exceção, `cq-social-translation` o pacote está faltando no arquivo [!DNL Experience Manager] 6.5 UberJar (NPR-31186).
* As bibliotecas de Jackson Databind foram atualizadas para a versão 2.9.9.3 para endereçar novas vulnerabilidades (NPR-30967).
* Os títulos Atividades e Notificações são inconsistentes (NPR-30941).
* Pagination is not working properly in [!DNL Communities] Blogs (NPR-30914).
* Analytics reports are not populated in [!DNL Experience Manager] author environment, blank page appears (NPR-30913).

### Oak {#oak}

* Atualizações de índice Lucene fazendo com que o servidor do autor fique lento (NPR-31548).

### Forms {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] O Service Pack não inclui correções para [!DNL Experience Manager Forms]. Eles são entregues usando um pacote complementar separado do Forms. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. Para obter mais informações, consulte [Instalar o complemento](#install-aem-forms-add-on-package) Experience Manager Forms e [Instalar formulários Experience Manager no JEE](#install-aem-forms-jee-installer).

#### Pacote complementar do Forms {#forms-add-on-package-6530}

**Formulários adaptáveis**

* As strings contêm a chave do dicionário ao localizar formulários adaptáveis (NPR-31110).

**Comunicação interativa**

* **MissingNode.toString()** retorna resultados imprecisos após atualizar as bibliotecas Jackson para 2.10.0 (NPR-31549).

* O editor de texto remove aleatoriamente caracteres de espaço do texto copiado do Microsoft Word (NPR-31113).

**Gerenciamento de correspondência**

* As legendas e dicas de ferramentas não são exibidas durante a migração de letras do LiveCycle ES4SP1 para o [!DNL Experience Manager] 6.5 (NPR-31615).

* **A formatação do fluxo de texto não é mais exibida uma mensagem de erro compatível** ao salvar letras como rascunhos (NPR-30463).

**Fluxo de trabalho**

* O fluxo de trabalho do OSGi falha devido à utilização de 100% da CPU (NPR-31233).

**Formulários HTML5**

* Gerar a visualização HTML5 de um formulário XDP mostra uma oscilação ao adicionar instâncias de um formulário secundário (NPR-30909).

#### Formulários no instalador JEE {#forms-jee-installer-6530}

**Forms - Serviços de documentos**

* O serviço Web SOAP que usa MTOM em um projeto .NET exibe exceções para a chamada AssemblerServiceClient e métodos HtmlToPDF2 (NPR-4281771).

**Foundation JEE**

* A configuração de ação não carrega os nomes de processo para Chamar uma ação de envio do Forms Workflow (NPR-31478).

### Feature Packs incluídos {#feature-packs-included-6530}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Suporte a formulários para o Oracle 18c (NPR-29155).

## Adobe Experience Manager 6.5.2.0

[!DNL Adobe Experience Manager] 6.5.2.0 é uma versão importante que inclui correções e melhorias de desempenho, estabilidade, segurança e essenciais para o cliente lançadas desde a disponibilização geral do [!DNL Adobe Experience Manager] 6.5 em **abril de 2019**. It can be installed on top of [!DNL Experience Manager] 6.5.

Alguns destaques principais desta versão do Service pack:

* O repositório integrado (Apache Jackrabbit Oak) foi atualizado para a versão 1.10.3.
* Adição de uma propriedade de configuração para permitir a exportação de Fragmentos de experiência diretamente para espaços de trabalho definidos pelo usuário do [!DNL Adobe Target].
* Os usuários do Assets podem pesquisar imagens visualmente semelhantes. [!DNL Experience Manager]O exibe as imagens com tags inteligentes do repositório DAM que são semelhantes a uma imagem selecionada pelo usuário. Consulte [pesquisa visual](../assets/search-assets.md#visualsearch).

* Aprimoramento da funcionalidade Ativos conectados para adicionar suporte à busca de documentos a partir de implantações remotas do DAM. Os autores do site agora podem pesquisar e filtrar tipos de documentos compatíveis no Localizador de conteúdo. Os documentos remotos podem ser adicionados ao Componente de download em páginas da Web. Consulte [usar ativos conectados](../assets/use-assets-across-connected-assets-instances.md).

* Aprimorarfiltros do tipo Document com mais tipos MIME para suportar opções de vários valores.
* Introdução de um fluxo de trabalho externo de reprocessamento para oferecer suporte a vários recursos.
* Desempenho otimizado [!DNL Dynamic Media] usando filtros de ativos padrão para replicação.
* Restauração das opções de edição de cortar/girar ativos para o DMS7.
* Implementação de uma opção para silenciar um vídeo quando carregado no VideoPlayer.
* Correção para garantir que a exibição da coluna da interface do usuário do ativo mostre somente conteúdo específico do locatário.
* Correção para permitir que as alterações de acordeão de estilo reflitam nos resultados de pesquisa.

### Ativos {#assets}

**Aprimoramentos do produto**

* Aprimoramento da funcionalidade Ativos conectados para adicionar suporte à busca de documentos a partir de implantações remotas do DAM. Os autores do site agora podem pesquisar e filtrar tipos de documentos compatíveis no Localizador de conteúdo. Os documentos remotos podem ser adicionados ao Componente de download em páginas da Web. Hotfix do CQ-4270245. Consulte [usar ativos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Experience Manager Assets]Os usuários do podem pesquisar imagens visualmente semelhantes. [!DNL Experience Manager]O exibe as imagens com tags inteligentes do repositório DAM que são semelhantes a uma imagem selecionada pelo usuário. Consulte [pesquisa visual](../assets/search-assets.md#visualsearch).

**Correções**

* Os caminhos de ativos nos metadados de URLs e de pastas gerados pela API ACP não são codificados por URL. GRANITE-26198: Hotfix do CQ-4271814
* Unzipping an archive with a folder having a percent sign (%) in its name can not be opened using [!DNL Experience Manager Assets] interface. NPR-29989: Hotfix do CQ-4270467
* Interface do usuário para toque: Durante o assistente de gerenciamento de publicação, as referências são adicionadas após a página no corpo da solicitação de publicação, fazendo com que todos os ativos sejam publicados após a página e, quando a página for renderizada, alguns dos ativos na instância de publicação serão perdidos. NPR-29985: Hotfix do CQ-4270724
* O recurso Ativo não relacionado não funciona para ativos relacionados que têm caracteres especiais (caracteres que se tornam codificados por URI) no nome. NPR-30387: Hotfix do CQ-4274446
* Ao editar um fragmento do conteúdo, a versão é criada com o usuário errado.
* Falha durante a criação de coleções no sistema baseado em Locatário. NPR-30114: Hotfix do CQ-4272948
* A exibição em coluna da interface do usuário do ativo não respeita o caminho DAM raiz do locatário atual, mas acessa todos os caminhos DAM do locatário. NPR-30636: Hotfix do CQ-4275481
* Possível ataque de script entre sites (XSS) por meio da janela de alerta de arquivo restrito, pois a imagem injetada pode ser vista. NPR-30617: Hotfix do CQ-4270133
* MultiTenant: Os locatários que salvam as propriedades da pasta observam o prompt de sucesso e a mensagem de erro que descreve a ação não foi bem-sucedida. &quot;Não é possível editar as propriedades. Permissões insuficientes.&quot; Os confundido. NPR-30545: Hotfix do CQ-4275333
* A caixa de diálogo do seletor de ativos não permite a seleção de ativos. Portanto, não é possível atualizar a fonte usando a funcionalidade de substituição da fonte relacionada. NPR-30502: Hotfix do CQ-4275029
* Fluxo de trabalho do ativo de atualização DAM - no estado obsoleto ao carregar arquivos mp4 de tamanho grande. NPR-30480: Hotfix do CQ-4271352
* A funcionalidade Criar tarefa de revisão não funciona devido a uma carga nula que faz com que todas as ações subsequentes relacionadas à tarefa de revisão falhem. NPR-30468: Hotfix do CQ-4274263
* Problema de conectividade com o Adobe Smart Tag por meio do Datapower. NPR-30026: Hotfix do CQ-4269457
* A exibição em coluna da interface do usuário do Assets emite um erro ao tentar abrir os filtros que saíram do painel. NPR-30501: Hotfix do CQ-4273862
* Ao adicionar grupos sincronizados do LDAP nas propriedades de Grupo de usuários fechado (CUG) de uma Pasta de ativos, o grupo não é salvo e recuperado. NPR-30615: Hotfix do CQ-4274689
* Os campos de estilo de pesquisa e orientação de filtros não aplicam o valor preenchido automaticamente à consulta de pesquisa. NPR-30620: Hotfix do CQ-4275724
* O link de compartilhamento de ativos de uma pasta com espaço e o caractere &quot;&amp;&quot; no nome exibe cartões cinza em branco para alguns ativos. NPR-30557: Hotfix do CQ-4270187
* O formulário de esquema de metadados da pasta não detecta automaticamente o tipo de dados e, portanto, não cria o TypeHint relacionado no envio do formulário. NPR-30599: Hotfix do CQ-4275227
* As opções de edição Recortar e Girar do ativo estão desativadas na interface do usuário de criação do DMS7. NPR-30118: Hotfix do CQ-4273221
* Share Link feature is not working on [!DNL Experience Manager] instance with DMS7 configuration. NPR-30080, NPR-30492: Hotfix do CQ-4273651
* Adding the [!DNL Dynamic Media] Scene7 component to the page, and then publishing the page does not trigger the dmscene7 configuration every time. NPR-30641: Hotfix do CQ-4275962
* Added an IPSJobJournal in [!DNL Experience Manager] to create only one Intrusion Prevention Systems (IPS) job per processing profile. NPR-30490: Hotfix do CQ-4273614
* [!DNL Dynamic Media]: Adicionados filtros padrão para excluir ativos de serem replicados para o nó de [!DNL Experience Manager] publicação. NPR-30538: Hotfix do CQ-4274678
* Introdução de um fluxo de trabalho externo de reprocessamento para suporte a vários recursos de forma a permitir a pasta como uma carga. O fluxo de trabalho tem duas etapas: reprocessa ativos não manuseados pelo mapa de metadados para a próxima etapa e recarrega todos os ativos não manuseados para S7 em um único trabalho IPS. For more details, see Configuring [!DNL Dynamic Media] Cloud Services. NPR-30489: Hotfix do CQ-4272903
* Carregar um CSV incorreto após o CSV correto apaga o CSV correto. Hotfix do CQ-4277694, CQ-4277814
* O ícone incorreto específico das pastas de contribuição a serem removidas. Hotfix do CQ-4277580
* Ao selecionar um usuário no seletor de usuários da guia Contribuição do ativo, o nome do usuário não aparece na tabela e a caixa de diálogo Excluir usuário na página de propriedades mostra o texto errado. Hotfix do CQ-4277875
* Os contribuidores não podem ser adicionados à pasta de contribuição do ativo no seletor de usuários ao selecionar o usuário e clicar em adicionar. Hotfix do CQ-4277824, CQ-4278087
* A pesquisa por nome de usuário em letras minúsculas não funciona no seletor de usuários. Hotfix do CQ-4277958, CQ-4277930
* Os não administradores podem publicar ativos em uma nova pasta de uma pasta de contribuição de ativos. Hotfix do CQ-4278200
* O dam-user (não administrador) não tem a opção de adicionar contribuidores à pasta de contribuição do ativo. Hotfix do CQ-4278192
* O botão &quot;Criar&quot; está visível na pasta Contribuição do ativo. Hotfix do CQ-4277560
* Sorting search query by relevance returns [!DNL InDesign] documents along with [!DNL InDesign] templates. Hotfix do CQ-4273864
* Se o usuário tiver uma ID de email em letras maiúsculas, os usuários não poderão fazer check-in nos ativos cujo check-out foi feito anteriormente. Hotfix do CQ-4276575
* A operação Excluir se aplica somente às predefinições selecionadas e, se a tela atualizar automaticamente a lista após a operação, ela mostrará outras predefinições que já foram atualizadas. Hotfix do CQ-4261461
* Configuring [!DNL Dynamic Media] Cloud Services in DMHybrid mode results in multiple empty report suites created in [!DNL Analytics], and with no report suite id stored in [!DNL Experience Manager], resulting in report suite duplication. Hotfix do CQ-4249780
* Rename operation in [!DNL Experience Manager] asset to duplicated name fails to synchronize to Scene7. Hotfix do CQ-4276763
* O conteúdo gerado pelo usuário é exibido incorretamente no painel Filtro de pesquisa. Hotfix do CQ-4273875
* A opção Localizar semelhante não está disponível para imagens TIFF. Hotfix do CQ-4278238
* Implementação da opção para silenciar o vídeo quando carregado no VideoPlayer. Hotfix do CQ-4266465
* Visualizadores - Visualizador de vídeo: poster=none funciona incorretamente no caso de um vídeo externo ser usado. Hotfix do CQ-4265536
* O ícone Aguardar fica visível durante a reprodução do vídeo nos navegadores IE11 e MS Edge. Hotfix do CQ-4251539
* Os arquivos README dos visualizadores 3.8 e 5.13 não são atualizados e contêm informações de versões anteriores. Hotfix do CQ-4273737
* O Fragmento do conteúdo recebe controle de versão mesmo antes de salvar as alterações. NPR-30616: Hotfix do CQ-4273088
* Substitua Asset#getMetadata(String) por Asset#getMetadataValueFromJcr(String) no processo de miniatura. NPR-30491: Hotfix do CQ-4273067
* O upload do jpg causa várias instâncias da mensagem: &quot;ReplicateOnModifyWorker Replicating UPDATED&quot; para cada ativo, causando degradação do desempenho.
* Descompactar o arquivo zip usando o recurso &#39;Extrair arquivo&#39; causa problemas nas pastas cujo nome contém a porcentagem (%) no título. NPR-29990: Hotfix do CQ-4270467

### Sites {#sites-6520}

* Se a herança do LiveCopy for quebrada, as páginas de Live Copy exibirão links de cópia de idioma em vez de links do LiveCopy. (NPR-30980)
* Para um novo Blueprint, se o número de registros for superior a 40, somente os primeiros 40 registros serão exibidos. O Blueprint exibe linhas em branco para o restante dos registros. (NPR-31182)
* O plug-in do Editor de Rich Text (RTE) do componente de texto exibe caracteres distorcidos para o texto em japonês e coreano. (NPR-31331)
* O Editor de Rich Text (RTE) não permite inserir uma Tabela incorporada como um item de lista. (NPR-30879)
* O ERT (Editor de Rich Text) é aplicado inesperadamente ao tamanho da fonte em linha aos elementos. (NPR-31284)
* Quando um usuário foca nos campos do painel esquerdo e usa o atalho do teclado para colar o conteúdo, ele cola o conteúdo da área de transferência do editor de páginas em vez do conteúdo copiado dos campos do painel esquerdo. (NPR-31172)
* Quando um usuário adiciona um campo Upload de arquivo a um campo múltiplo, o caminho da imagem é armazenado no nó do componente em vez do nó de vários campos. (NPR-30882)
* A API ResponsiveGridExporter não retorna a interface com.day.cq.wcm.Foundation.model.impl.export.AllowedComponentsExporter. O pacote com.day.cq.wcm.Foundation.model.impl é declarado como pacote privado. (NPR-31398)
* Quando uma página que contém alguns Fragmentos de experiência é aberta no modo não editor (em Autor sem o `editor.html` prefixo e `wcmmode=disabled`, ou no Editor), a solicitação termina no código de erro de status HTTP 500. (NPR-30743)

### WCM - Editor de páginas {#wcm-page-editor-6520}

**Aprimoramentos do produto**

* Aprimorarfiltros do tipo Document com mais tipos MIME para suportar opções de vários valores. Hotfix do CQ-4270694

### Gerenciamento de fragmentos de conteúdo {#content-fragment-management-6520}

* A consulta usada pela interface do usuário de modelos do Fragmento do conteúdo é muito lenta e, eventualmente, resulta em um erro. Hotfix do CQ-4270807

### IU - Foundation {#ui-foundation}

* Os atalhos são acionados o que impede que o usuário use &#39;m,&#39; &#39;p,&#39; &#39;e&#39; em interfaces do usuário específicas. NPR-30355: Hotfix do GRANITE-26346
* Closing [!DNL Experience Manager Assets] Search UI does not reset the left rail to Content selection preventing the user from opening the filter rail the second time subsequently. NPR-30509: Hotfix do CQ-4274716
* Multi-tenant environment: [!DNL Experience Manager Assets] UI top navigation is not available and throwing JavaScript error. NPR-30104: Hotfix do GRANITE-26344

### Tradução {#translation-6520}

* Problema de tradução - somente alguns componentes estão sendo traduzidos pela tradução automática. NPR-30079: Hotfix do CQ-4273764

### Plataforma {#platform-6520}

* [!DNL Experience Manager]O remetente de email padrão do não pode enviar emails para um servidor SMTP remoto por TLS v1.2. NPR-30476: Hotfix do GRANITE-26605

### Projetos {#projects-6520}

* Os valores dam:folderThumbnailPaths não são atualizados e exibem miniaturas antigas mesmo depois de excluir os ativos dentro da pasta. NPR-30424: Hotfix do CQ-4273667
* Ao concluir a opção &quot;mover&quot;, o Título e o Nome do ativo permanecem inalterados. NPR-30647: Hotfix do CQ-4276265

### Communities {#communities-6520}

* O Diagnóstico de sincronização do usuário está completamente quebrado e falha ao funcionar. NPR-30004, NPR-29943: Hotfix do CQ-4270287, CQ-4271348

### Sling {#sling}

* A atualização da instância de 6.3.3.2 para 6.5 resulta em configurações OSGi duplicadas. NPR-30130: Hotfix do CQ-4274016

### Integração {#integration}

* O conteúdo personalizado não é exibido corretamente na instância de publicação até a reinicialização da instância. NPR-30377: Hotfix do CQ-4273706
* Ao configurar o Launch em um site, o endereço da biblioteca tem uma barra (/) anexada, sempre causando intervenção manual. NPR-30694: Hotfix do CQ-4275501

### Forms {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] O Service Pack não inclui correções para [!DNL Experience Manager Forms]. They are delivered using a separate [!DNL Forms] add-on package. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. For more information, see [Install Experience Manager Forms add-on](#install-aem-forms-add-on-package) and [Install Experience Manager Forms JEE installer](#forms-jee-installer).

The key highlights for [!DNL Experience Manager] 6.5.2.0 forms are:

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager] Forms OSGi.

#### Pacote complementar do Forms {#forms-add-on-package}

**Integração back end**

* Não é possível configurar o Modelo de dados de formulário usando um URL com balanceamento de carga hospedado no AWS. NPR-30123: Hotfix do CQ-4273359
* Ao criar o Modelo de Dados de Formulário (FDM) com a Linguagem de Definição de Serviço da Web (WSDL), a mensagem de erro `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` é retornada: NPR-30477: Hotfix para CQ-4272921

**Gerenciamento de correspondência**

* &quot;A execução Criar interface do usuário de correspondência (CCR UI) falha intermitentemente com o erro abaixo no console:
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**Comunicação interativa**

* Um campo marcado como obrigatório no modelo de dados de formulário é exibido conforme solicitado em Criar interface do usuário de correspondência (CCR UI). NPR-30623: Hotfix do CQ-4274902

**Forms - Fluxo de trabalho**

* Variáveis de saída não mapeadas em Pastas vigiadas causam falha na chamada. Hotfix do CQ-4264451

**Formulários HTML5**

* Quando o código personalizado ou o projeto é implantado pela segunda vez, a página não é renderizada e o seguinte erro ocorre:

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539: Hotfix do CQ-4272509

* Ao usar o NonVisual Desktop Access no modo Procurar para ler um formulário HTML5, o navegador Chrome lê &quot;gráfico&quot; antes de cada Gráfico de vetor escalonável (SVG) no design do formulário. NPR-30449: Hotfix do CQ-4274732

#### Instalador do Forms JEE {#forms-jee-installer}

**Forms - Segurança de documentos**

* A aplicação de uma assinatura com carimbo de data e hora falha com erro: ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: erro de chamada. NPR-30820: Hotfix do CQ-4275852

**Forms - Serviços de documentos**

* Se &quot;SubmitURL&quot; contiver um E comercial (&amp;), aparecerão erros de análise no registro quando a solicitação POST for feita para renderpdf servlet. NPR-30865: Hotfix do CQ-4278232

**Forms - Foundation JEE**

* O serviço HTMLtoPDF não mostra maxReuseCount no console JMX. NPR-30134, NPR-30304: Hotfix do CQ-4273763
* Adding or editing a Web Service connection by invoking web services from [!DNL Experience Manager Forms] Workbench throws an error: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105: Hotfix do CQ-4273217

### Feature Packs incluídos {#feature-packs-included}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### Sites {#sites-feature-packs-included}

* Adição de uma propriedade de configuração para permitir a exportação de Fragmentos de experiência diretamente para espaços de trabalho definidos pelo usuário do [!DNL Adobe Target]. NPR-29189: Hotfix do CQ-4249782

#### Forms - Serviços de documentos {#forms-document-services-1}

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager Forms] OSGi. NPR-30759: Hotfix do CQ-4278193

## Adobe Experience Manager 6.5.1.0 {#release-6510}

[!DNL Adobe Experience Manager] 6.5.1.0 é uma versão importante que inclui correções e melhorias de desempenho, estabilidade, segurança e essenciais para o cliente lançadas desde a disponibilização geral do [!DNL Adobe Experience Manager] 6.5 em *abril de 2019.*[!DNL Experience Manager] Ele pode ser instalado por cima do 6.5.

Alguns destaques principais desta versão do Service pack:

* Habilitação da inclusão do estado da interface do usuário dinâmica em eventos de rastreamento como atributos personalizados.
* Included support for the delivery of 360-degree video assets in [!DNL Dynamic Media] Scene 7.
* Enabled *Japanese Word Wrap* feature via the styles plugin of Rich Text Editor. Para obter mais informações, consulte [Configurar quebra automática de texto em japonês](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Ativos

* Atualização da interface DAM DMGGateway para oferecer suporte a várias peças S3. NPR-29740: Hotfix do CQ-4226303
* A pré-visualização de execuções gera `Only empty tenantId is currently supported` erro após a atualização para [!DNL Experience Manager] 6.5. NPR-29986: Hotfix para CQ-4272353
* A caixa de diálogo Excluir não está visível para permitir a exclusão de trabalhos. NPR-29720: Hotfix do CQ-4271074
* After adding asset title in the properties page, when a user attempts to close the page, [!DNL Experience Manager] opens the properties page again. NPR-29627: Hotfix do CQ-4264929
* VersioningTimelineEventProvider deve fornecer a versão raiz juntamente com o nó do tipo nt: version. Hotfix do GRANITE-26063
* Implemented the ability to upload and play 360 spherical videos in [!DNL Experience Manager] DM-Scene7 mode. Hotfix do CQ-4265131
* A Live Copy recupera o status incorreto se a fonte for editada. Hotfix do CQ-4265451
* Ativação do suporte Multi-Site Manager no [!DNL Experience Manager Assets]. Hotfix do CQ-4271453, CQ-4268621, CQ-4257491
* [!DNL Experience Manager] deve exibir uma entrada adicional para a versão atual do ativo no histórico da linha do tempo, exibindo o comentário de check-in mais recente do [!DNL Adobe Asset Link]. Hotfix do CQ-4262864
* A Linha do tempo do fragmento do conteúdo exibe uma mensagem de erro quando as propriedades estão ausentes. Hotfix do CQ-4272560
* Um problema com o reprodutor de vídeo do Scene 7 quando expandido para tela cheia. Hotfix do CQ-4266700
* ZoomVerticalViewer: os botões de deslocamento não devem ser exibidos se um único ativo de imagem for usado. Hotfix do CQ-4264795
* A exclusão de um nó secundário na live copy deve desanexar o liveRelationship. Hotfix do CQ-4270395
* O esquema de metadados contém apenas itens da configuração global, e não os itens do locatário ativo. O valor de URL formPath é revertido para o padrão mesmo quando alterado. NPR-29945: Hotfix do CQ-4262898
* Publish image presets to [!DNL Brand Portal] fails with 500 error code. NPR-29510: Hotfix do CQ-4268659

### Sites

* Propriedades vazias e várias propriedades não se propagam a partir do blueprint durante o lançamento. A redefinição da live copy com blueprint não funciona em componentes. NPR-29253: Hotfix do CQ-4264928, CQ-4264926, CQ-4267722
* CoralUI, when used with `Multifield`, stores the `fileReferenceParameter` at the component level instead of multifield level. NPR-29537: Hotfix do CQ-4266129
* Enhancement of [!DNL Experience Manager] text component and Text Editor to Japanese. NPR-29785: Hotfix do CQ-4265090
* A página restaurada com o Timewarp deve se referir à imagem correta no momento do controle de versão. NPR-29431: Hotfix do CQ-4262638
* Um problema com a herança dos nós do Sistema de estilo do pai para o filho. NPR-29516: Hotfix do CQ-4270330
* An error message while setting up the social posting to [!DNL Facebook] authentication. NPR-29211: Hotfix do CQ-4266630
* A miniatura renderizada no Fragmento do conteúdo mostra a representação interna do calendário do campo Data e hora. NPR-29531: Hotfix do CQ-4269362
* Abrir a guia de permissões na implementação do Coral2 não mostra os botões. Hotfix do CQ-4269419

### Comércio

* ConstraintViolationException, ao executar migração de conteúdo lento para comércio eletrônico. NPR-29247: Hotfix do CQ-4264383

### Gerenciamento de fragmentos de conteúdo

* Parsing error when opening a Content Fragment which has characters dollar `($)` and open brace `({)`. Hotfix do CQ-4270266

### Fragmentos de experiência

* Exportar [!DNL Experience Manager] fragmentos de experiência para [!DNL Adobe Target]. Hotfix do CQ-4265469
* A exportação de Fragmentos de experiência para o público alvo falha com a imagem inteligente. Hotfix do CQ-4269606

* O usuário atinge um beco sem saída quando tenta mover os Fragmentos de experiência pelo Omnisearch na exibição de cartão. Hotfix do CQ-4263848

### WCM - Editor de páginas

* Script entre sites (XSS) refletido ao usar um seletor inválido. Hotfix do CQ-4270397

### Replicação

* Os dados fornecidos pelo usuário não são escapados na saída no componente `cq/replication/components/agent`, resultando em uma vulnerabilidade de script entre sites (XSS). Hotfix do CQ-4266263

### Fluxo de trabalho

* Campo de seletor de calendário do participante na caixa de diálogo quebrado. NPR-29727: Hotfix do CQ-4270423

### WCM - Editor SPA

* Ativação da busca de conteúdo pré-renderizado a partir de um endpoint remoto. Hotfix do CQ-4270238
* Avisos em registros ao abrir uma Página de modelo SPA renderizada no lado do servidor. Hotfix do CQ-4270238

### WCM - MSM

* Upgrade to [!DNL Experience Manager] 6.4.3 makes Multi-Site Manager take a long time to roll out. Hotfix do CQ-4271410

### Integração

* As credenciais do BrightEdge falham com erro de conexão. NPR-29168: Hotfix do CQ-4265872

* An exception message is displayed when trying to edit and save the [!DNL Experience Manager] launch configuration. NPR-29176: Hotfix do CQ-4265782/CQ-4266153

### Interface do usuário

* Adição de suporte para rastrear estados dinâmicos de interface do usuário como atributos personalizados ao rastrear determinados eventos na API de rastreamento de base. Hotfix do GRANITE-26283
* Não é possível definir o recurso de rastreamento no botão Enviar. Hotfix do GRANITE-26326
* O assistente não pode definir o recurso de rastreamento no botão Enviar. NPR-29995, NPR-30025: Hotfix do CQ-4264289

### Communities

* Não é possível alinhar novos selos na lista suspensa da página de perfil do membro. NPR-29381: Hotfix do CQ-4267987
* Os visitantes e membros, sem privilégios de moderador, podem ver publicações não aprovadas/pendentes ao colar o URL. NPR-29724: Hotfix do CQ-4271124, CQ-4271441
* É observado um tempo de resposta alto de 40 a 50 segundos no logon do usuário na Comunidade. NPR-29677: Hotfix do CQ-4269444

### Replicação

* O componente Replication Agent é susceptível a uma vulnerabilidade que exibe informações confidenciais para usuários não autorizados. NPR-29611: Hotfix do GRANITE-25070

* Vazamento de sessão durante o OAuth em cada replicação no [!DNL Brand Portal]. NPR-30001: Hotfix do GRANITE-26196

### Projetos

* Publish [!DNL Experience Manager Assets] from [!DNL Experience Manager] Author /content/dam/mac folder to [!DNL Brand Portal] doesn&#39;t work. NPR-29819: Hotfix do CQ-4271118

### Plataforma

* HtmlLibraryManager exclui todo o conteúdo de crx-quickstart na invalidação do cache. NPR-29863: Hotfix do GRANITE-26197

### Felix

* Os detalhes de uso de memória não sãp exibidos no console do sistema ao usar o Java11\. NPR-29669

### Forms

The key highlights for [!DNL Experience Manager Forms] 6.5.1.0 are:

* OSGi only: Added a new attribute `PAGECOUNT` in Output and Forms Service.

* Apenas OSGI: Ativado o suporte para criar arquivos PDF estáticos usando o Forms Service.
* Ativação das permissões no XMLForm.exe para administradores e usuários raiz.
* Ativação de suporte para ADFS v3.0 para integração local do Dynamics.

#### Pacote complementar do Forms

**Integração de backend**

* Falha ao obter a Linguagem de definição do serviço da Web (WSDL). NPR-29944: Hotfix do CQ-4270777
* When [!DNL Experience Manager Forms]  is installed on IBM WebSphere, creating a form data model based on SOAP fails. Hotfix do CQ-4251134
* Ativação de suporte para o Ative Diretory Federation Services (ADFS) v3.0 para integração local do Microsoft Dynamics. Hotfix do CQ-4270586
* Quando o título de uma fonte de dados é alterado, o modelo de dados do formulário não exibe o título atualizado. Hotfix do CQ-4265599
* Se o nome de uma entidade ou atributo contiver hífen ou espaço, o expressão não avaliará essas entidades e atributos. Hotfix do CQ-4225129

* A saída incorreta é observada quando um dois pontos está presente na saída da string primitiva. Hotfix do CQ-4260825

* Mesmo quando nenhum conteúdo é esperado da saída da API REST, a operação de chamada do modelo de dados de formulário emite um erro. Hotfix do CQ-4268828

**Formulários adaptáveis**

* Não é possível adicionar uma nova instância no Fragmento de formulário adaptável durante o carregamento lento. NPR-29818: Hotfix do CQ-4269875
* Verifique se o componente não registra ou exibe algum erro nos modelos de Documento de registro. Hotfix do CQ-4272999
* Adição de suporte para desativar o editor de layout para Adaptive Forms. Hotfix do CQ-4270810
* Restored the verify step for Adaptive Forms in [!DNL Experience Manager] 6.5. Hotfix for CQ-4269583

* Adaptive Form field validation failure breaks [!DNL Adobe Sign]. Hotfix do CQ-4269463
* When an [!DNL Experience Manager Forms] instance has more than 20 adaptive form fragments and name of all the form fragments starts with the same string, the search returns no or only recent 20 created fragments. Hotfix do CQ-4264414, CQ-4264914

* Problemas de desempenho quando o aplicativo Adaptive Forms é usado com um conjunto de dados grande. . Hotfix do CQ-4235310

* Quando acessado por meio de uma conta anônima em uma instância de publicação, o script GuideRuntime não é carregado. Hotfix do CQ-4268679

**Forms - Comunicação interativa**

* O modelo de comunicação interativa não lista componentes de cabeçalho e rodapé na lista de componentes permitidos. Hotfix do CQ-4237895
* Ao criar um modelo de impressão de comunicação interativa contendo um campo de imagem, o título do gráfico é definido como em branco. Hotfix do CQ-4264772
* A cor da linha de um gráfico, quando excluída, é definida como indefinida. Hotfix do CQ-4264762
* As alterações na camada de layout feitas no Fragmento do Documento desaparecem ao executar manter as alterações sincronizadas. Hotfix do CQ-4266054
* O elemento do modelo de dados de formulário dentro de um Fragmento do documento vinculado a um campo de texto não mostra o ícone de herança e permite combinação. Hotfix do CQ-4261089
* A API de renderização do Canal de impressão não tem a opção de transferir dados como parâmetro na API. Hotfix do CQ-4263540
* As configurações do agente não estão visíveis, pois a caixa de seleção Editável pelo agente fica desmarcada quando o tipo de vínculo é alterado do fragmento de texto para Nenhum/Objeto de modelo de dados para o campo/variável String. Hotfix do CQ-4261953
* No envio da interface do agente, o arquivo json de dados da Web resultante armazena informações para campos não vinculados cancelados por herança. Hotfix do CQ-4265621

**Forms - Fluxo de trabalho**

* Quando um formulário é reenviado da caixa de saída do aplicativo Adaptive Forms, isso resulta em perda de dados. NPR-28345: Hotfix do CQ-4260929
* Os documentos não são fechados ao salvar em casos não variáveis. Hotfix do CQ-4269784
* O aplicativo Adaptive Forms deixou de oferecer suporte ao Microsoft Windows 8.1. Hotfix do CQ-4265274
* When an image of more than 2 MB is attached as a field level attachment to a form in the Android version of [!DNL Experience Manager Forms] app, the app crashes. Hotfix do CQ-4265578

* Ativação das opções de pré-preenchimento para o canal de impressão de comunicação interativa na tarefa Atribuir. Hotfix do CQ-4265577
* Os usuários não poderão visualizar uma tarefa compartilhada até que se tornem membros do grupo ao qual a tarefa está atribuída. Hotfix do CQ-4248733
* Salvar ou enviar aplicativos JEE no aplicativo Adaptive Form está bloqueado no Windows. Hotfix do CQ-4268704
* O modelo de dados de formulário associado à variável do modelo de dados de formulário não é visível. Hotfix do CQ-4266554
* Não há suporte para a variável de status de assinatura do documento usando o suporte à variável. Hotfix do CQ-4266312
* Os envios a partir do espaço de trabalho falham com um caractere de trema. Hotfix do CQ-4263172
* Em uma configuração atualizada, se o fluxo de trabalho for aberto para edição, um erro será exibido em vez do nome do fluxo de trabalho na interface do usuário da pasta monitorada (UI). Hotfix do CQ-4238579

**Forms - Gerenciamento**

* Quando uma extensão diferente de xsd ou schema.json é carregada, o upload não ocorre e nenhuma mensagem de erro é gerada. Hotfix do CQ-4266716

**Forms - Gerenciamento de correspondência**

* [!DNL Experience Manager Forms] 6.5 Falha ao criar interface de usuário de correspondência (CCR UI) ao abrir a correspondência criada com [!DNL Experience Manager Forms] 6.3. Hotfix para CQ-4266392
* A função de soma no XDP não funcionará se o tipo de dados DDE for do tipo número. Hotfix do CQ-4227403
* Faz com que a lógica de invalidação do cache na memória seja atualizada porque, quando um ativo é publicado, o horário da última modificação não é atualizado. Hotfix do CQ-4250465
* Não é possível publicar o fragmento do documento, DD &amp; Letters. Hotfix do CQ-4272893

#### Instalador do Forms JEE

**Gerador de PDF**

* Os arquivos CAD para conversão em PDF falham com o JDK de 64 bits. NPR-29924, NPR-29925: Hotfix do CQ-4272113
* Substituição do nome de PhantomJS para WebToPDF para conversão de HTML em PDF. NPR-29933: Hotfix do CQ-4234545
* Um erro é gerado ao converter o arquivo zip em PDF. Hotfix do CQ-4268628

**Forms - Designer**

* When a full accessibility check is performed on the static PDF created using [!DNL Experience Manager Forms Designer], the Primary Language check fails due to missing language attribute. Hotfix do CQ-4272923, CQ-4271002

**Forms - Segurança de documentos**

* A Assinatura digital com o Módulo de segurança de hardware (HSM) não está funcionando no OSGi Linux no Java 11 e Java 8\. NPR-29838: Hotfix do CQ-4270441
* A assinatura digital com o Módulo de segurança de hardware (HSM) não está funcionando no JEE Linux e em todos os servidores de aplicativos compatíveis, ou seja, JBoss e Webphere. NPR-29839: Hotfix do CQ-4266721
* A verificação de assinaturas em um PDF usando o PDF Advanced Electronic Signatures (PAdES) gera InvalidOperationException. NPR-29842: Hotfix do CQ-4244837
* Adição do suporte à Extensão de segurança de documento para o Office 2019\. Hotfix do CQ-4254369, CQ-4259764

**Forms - Serviços de documentos**

* Falha na conversão de PDF em PDF/A-1b com o campo Formulário sem dict de aparência. NPR-29940: Hotfix do CQ-4269618

* OSGi: Não é possível determinar o número de páginas geradas durante a renderização. NPR-28922: Hotfix do CQ-4270870
* Ativado o suporte para arquivos PDF estáticos usando o Forms Service em [!DNL Experience Manager Forms OSGi]. NPR-28572: Hotfix do CQ-4270869
* Não é possível alterar as permissões em XMLForm.exe. NPR-29828, NPR-29237: Hotfix do Q-4267080
* The static PDF created by the [!DNL Experience Manager Forms] server’s output module does not populate the language attribute/tag with the language of the document created. NPR-27332: Hotfix do CQ-4271002

**Forms - Foundation JEE**

* O pdfg_srt indisponível em artefatos finais faz com que o instalador falhe. NPR-29854: Hotfix do CQ-4270137
* LCBackupMode.sh não está funcionando. NPR-29840: Hotfix do CQ-4269424
* A referência de porta UDP deve ser removida da interface do usuário (UI) do WebSphere. Hotfix do CQ-4264782

### Feature Packs incluídos

#### Ativos - Incluídos

* Ativação do suporte Multi-Site Manager no [!DNL Experience Manager Assets]. For more information, see [Reuse assets using MSM for Experience Manager Assets](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html). NPR-29199: Hotfix do CQ-4259922

#### Sites - Incluídos

* Exportar [!DNL Experience Manager] fragmentos de experiência para [!DNL Adobe Target]. For more details, see [The Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Hotfix do CQ-4265469

#### Forms - Serviços de documentos - Incluído

* Somente OSGi: Adicionado um novo atributo PAGECOUNT no Serviço de saída e formulários. NPR-28922: Hotfix do CQ-4270870
* Somente OSGi: Ativado o suporte para criar arquivos PDF estáticos usando o Forms Service. NPR-28572: Hotfix do CQ-4270869
* Ativação das permissões no XMLForm.exe para administradores e usuários raiz. NPR-29237: Hotfix do CQ-4267080

### Pacotes de conteúdo e pacotes OSGi

The following text documents list the OSGi bundles and Content Packages included in [!DNL Experience Manager] 6.5.1.0

List of OSGi bundles included in [!DNL Experience Manager] 6.5.1.0

[Obter arquivo](assets/6_5-bundle-list.txt)

List of Content Packages included in [!DNL Experience Manager] 6.5.1.0

[Obter arquivo](assets/6_5-content-package-list.txt)
