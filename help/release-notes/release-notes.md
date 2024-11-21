---
title: Notas de versão do  [!DNL Adobe Experience Manager] 6.5
description: Encontre informações sobre a versão, novidades, instruções de instalação e uma lista de alterações detalhada para o [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 9026b6777e4c3f030eae37491c823a68afe61270
workflow-type: tm+mt
source-wordcount: '5027'
ht-degree: 1%

---

# Notas de Versão do Service Pack Mais Recente do [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informações da versão {#release-information}

| Produto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.22.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versão do Service Pack |
| Data | Quinta-feira, 21 de novembro de 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## O que está incluído em [!DNL Experience Manager] 6.5.22.0 {#what-is-included-in-aem-6522}

O [!DNL Experience Manager] 6.5.22.0 inclui novos recursos, importantes melhorias solicitadas por clientes e correções de erros. Ele também inclui melhorias de desempenho, estabilidade e segurança lançadas desde a disponibilização inicial do 6.5, em abril de 2019. [Instalar este Service Pack](#install) em [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Principais recursos e melhorias

Os principais recursos e aprimoramentos desta versão incluem:

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

### Sites {#sites}

[O Universal Editor](/help/sites-developing/universal-editor/introduction.md) agora está disponível no AEM 6.5 para casos de uso headless com a aplicação de um pacote de recursos.

### [!DNL Assets]

A guia IPTC agora oferece suporte aos campos de texto [!UICONTROL Texto Alt] e [!UICONTROL Descrição Estendida]. (ASSETS-34918)

### [!DNL Forms]

* **Suporte para Credenciais OAuth**: uma credencial nova e mais fácil de usar para autenticação de servidor para servidor, substituindo a credencial de Conta de Serviço (JWT) existente. (NPR-41994)
* [Aprimoramentos do Editor de regras no AEM Forms](/help/forms/using/rule-editor-core-components.md):
   * Suporte para implementar condições aninhadas com funcionalidade `When-then-else`.
   * Validar ou redefinir painéis e formulários, incluindo campos.
   * Suporte para recursos modernos do JavaScript, como funções de seta e esquerda (suporte para ES10) nas Funções personalizadas.
* [API de marca automática para acessibilidade de PDF](/help/forms/using/aem-document-services-programmatically.md#doc-utility-services-doc-utility-services): o AEM Forms no OSGi agora oferece suporte à nova API de marca automática para aprimorar o PDF para padrões de acessibilidade adicionando marcas: parágrafos e listas. Isso torna os PDF mais acessíveis para usuários com tecnologia assistiva.
* **Suporte a PNG de 16 bits**: o serviço PDF Generator ImageToPdf agora oferece suporte à conversão de PNGs com intensidade de cor de 16 bits.
* **Aplicar artefatos a blocos de texto individuais em XDPs**: o Forms Designer agora permite que os usuários definam configurações em blocos de texto individuais em arquivos XDP. Essa capacidade permite controlar os elementos que são tratados como artefatos nos PDF resultantes. Esses elementos, como cabeçalhos e rodapés, são acessíveis para as tecnologias assistivas. Os principais recursos incluem marcar blocos de texto como artefatos e incorporar essas configurações nos metadados XDP. O serviço Forms Output aplica essas configurações durante a geração do PDF, garantindo a marcação adequada de PDF / UA.
* **O AEM Forms Designer é certificado com o `GB18030:2022` padrão**: com a certificação `GB18030:2022`, agora o Forms Designer oferece suporte ao conjunto de caracteres Unicode chinês que permite inserir caracteres chineses em todos os campos editáveis e caixas de diálogo.
* O serviço PDF Generator no servidor JEE agora [oferece suporte à rota WebToPDF](/help/forms/using/admin-help/configure-service-settings.md#generate-pdf-service-settings-generate-pdf-service-settings) para converter HTML em PDF, juntamente com as rotas WebKit existentes e WebCapture somente para Windows. Embora a rota WebToPDF já esteja disponível no OSGi e seja estendida para JEE. Agora, nas plataformas JEE e OSGi, o serviço PDF Generator suporta as seguintes rotas em diferentes sistemas operacionais:
   * **Windows**: WebKit, WebCapture, WebToPDF
   * **Linux®**: WebKit, WebToPDF

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Correção de problemas no Service Pack 22 {#fixed-issues}


### [!DNL Sites]{#sites-6522}


#### Acessibilidade {#sites-accessibility-6522}

* O botão seletor de amostra de anotação não tinha um nome acessível. Ou seja, usando um leitor de tela, não há nome compreensível para humanos para o botão selecionar após inserir um novo valor hexadecimal. (SITES-11992)
* Os seguintes elementos no menu do painel esquerdo aparecem como uma lista, mas não são marcados como tal no leitor de tela:

   * Site
   * Live Copy
   * Iniciar
   * Cópia de idioma
   * Pasta
   * Relatório CSV (SITES-2874)

* O Gerenciamento de conteúdo da Web principal do AEM requer um rótulo de acessibilidade para hiperlinks no Editor de Rich Text. Quando um hiperlink é usado no componente de texto, a marca de âncora deve incluir o atributo `aria-label` para garantir que os leitores de tela possam ler e transmitir o texto do link com precisão para fins de acessibilidade. (SITES-11511)
* No AEM, os elementos interativos no cabeçalho da tabela na Exibição de lista não têm a função de &quot;botão&quot; necessária. Dessa forma, o leitor de tela NVDA não anuncia as funções de botão esperadas para os seguintes cabeçalhos de tabela: Title, Name, Modified, Published, Preview, Template, Operation, Workflow. Cada elemento interativo no cabeçalho da tabela deve receber uma função de &quot;botão&quot; para garantir a compatibilidade com tecnologias assistivas como NVDA. (SITES-10962)


#### Interface do usuário do administrador{#sites-adminui-6522}

* Em alguns casos de AEM, as funcionalidades de visualização e comparação de versão não funcionavam como esperado em várias páginas. Especificamente:

   * **Problema de visualização:** Ao tentar visualizar uma versão da página, um erro aparece inicialmente. Depois de tentar novamente, a visualização resulta em uma página em branco.
   * **Problema de Comparação de Versões:** o recurso &quot;Comparar com Atual&quot; exibiu somente a versão atual, sem realçar diferenças entre as versões. (SITES-23988)

* Uma marca inesperada do `<br>` aparece no campo Editor de Rich Text (RTE) ao usar o `defaultPasteMode` definido como `plaintext` durante uma ação de copiar e colar. Esse problema resulta em diferentes marcações para o mesmo conteúdo, resultando no mesmo conteúdo de texto sendo traduzido duas vezes na memória de tradução de um cliente. (SITES-23606)
* No AEM 6.5.20.0, foi encontrado um problema de funcionalidade com o recurso **Gerenciar Publicação**. Ao selecionar um nó e agendá-lo para publicação futura, uma mensagem de erro — &quot;Falha ao recuperar recursos secundários de itens selecionados&quot; — pode ser exibida ao tentar incluir nós secundários. Esse problema bloqueava o uso da opção **Incluir Filhos**, impedindo a publicação completa da hierarquia de conteúdo desejada. (SITES-23000)
* O carimbo de data e hora &quot;Publicado&quot; de um modelo não era atualizado no ambiente do autor, mesmo que o modelo tivesse sido replicado com êxito para as instâncias de publicação. O comportamento esperado era que o carimbo de data e hora na instância do autor refletisse a publicação mais recente, mas essa atualização não estava ocorrendo conforme o esperado. (SITES-21585)
* Houve uma discrepância na contagem de Links recebidos no ambiente do autor do AEM. O painel lateral esquerdo mostrou menos links em comparação à interface clássica. Além disso, alguns Links de entrada que eram legítimos não funcionam. (SITES-24837)
* Tempos de carregamento extremamente longos estavam sendo relatados ao visualizar versões de página na exibição da Linha do tempo do AEM. Levava até 19 minutos para exibir versões. Esse problema estava em andamento desde a atualização do AEM 6.4.8 para o 6.5.18, interrompendo significativamente a eficiência do fluxo de trabalho. (SITES-22468 E SITES-22467)

<!-- #### Classic UI{#sites-classicui-6522} 

* A -->


#### [!DNL Content Fragments]{#sites-contentfragments-6522}

* No AEM 6.5.17 atualizado, salvar os Fragmentos de conteúdo resultou no seguinte erro: *ERRO: não foi possível salvar o Fragmento de conteúdo.* (SITES-22993)
* Um problema foi identificado com um resolvedor de recursos não fechado em `ContentFragmentModelOmniSearchHandler` no editor no AEM. (SITES-24903)


#### [!DNL Content Fragments] - Administrador{#sites-admin-6522}

Clicar no link na notificação por email direciona o usuário para o visualizador ou editor de ativos padrão. Isso é feito no lugar do editor de Fragmento de conteúdo, mesmo quando o ativo no fluxo de trabalho é determinado como um Fragmento de conteúdo. (SITES-24338)


#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6522}

Ao usar Fragmentos de conteúdo com itens de campo de Texto de várias linhas, a marcação gerada ao consultar usando o GraphQL não retinha a formatação conforme especificado no HTML. Por exemplo, uma nova linha estava ausente após a lista. O impacto foi que o último parágrafo passou a fazer parte da lista. (SITES-23233)


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6522}

* A


#### [!DNL Content Fragments] - REST API{#sites-restapi-6522}

* A -->

#### Infraestrutura principal{#sites-core-backend-6522}

* Erros `SegmentNotFoundException` recorrentes foram relatados em uma instância de autor AEM. Reiniciar o autor resolveu temporariamente o problema, mas uma correção de longo prazo foi necessária para evitar mais ocorrências. (SITES-22573)
* Foi gerado um problema sobre a funcionalidade de linha do tempo no AEM Sites, especificamente o tratamento de propriedades `cq:lastModified` ausentes em anotações. Após a aplicação do AEM 6.5.20, havia incerteza sobre se o conteúdo existente precisava de correção para a propriedade ausente ou se a linha do tempo foi atualizada para funcionar corretamente sem ela. (SITES-21861)


#### Componentes principais{#sites-core-components-6522}

* Após uma atualização do AEM 6.5.18 para o 6.5.21, um problema foi identificado com a funcionalidade que verifica o uso em tempo real dos componentes. Ao tentar rolar a tela para itens adicionais na página Uso em tempo real, a tabela não carregava mais resultados, mesmo que &quot;Carregar mais itens&quot; fosse visto na interface do usuário. (SITES-23919)
* Foi relatado um problema com a validação de campos obrigatórios em uma caixa de diálogo de componente AEM que contém duas guias. A guia 1 incluía um editor de rich text (RTE) e campos de texto, enquanto a guia 2 tinha campos de caminho e campos de texto. Embora todos os campos estejam marcados como obrigatórios (`required=true`), as notificações de erro persistem incorretamente na Guia 1, mesmo após o preenchimento de todos os campos obrigatórios. Por outro lado, os erros na guia 2 são apagados conforme esperado. (SITES-23243)
* Depois de migrar para AEM 6.5.21, a instrução `data-sly-include` da Linguagem de Modelo de HTML não funcionava mais conforme o esperado, especificamente não suportando expressões `appendPath` e `prependPath`. Como resultado, a saída do recurso incluído não era renderizada corretamente, mesmo que funcionasse corretamente antes da migração. Esse problema causava falhas de renderização para recursos que dependem dessas expressões para manipulação de caminho. (GRANITE-52970)


<!-- #### Campaign integration{#sites-campaign-integration-6522}

* A -->


#### Fragmentos de experiência{#sites-experiencefragments-6522}

* Os Fragmentos de experiência não são classificados por título conforme esperado quando o cabeçalho da coluna **Título** é clicado na Exibição de lista. Uma cintilação rápida da tela é observada, mas ela não é classificada. (SITES-23706)

* No AEM 6.5.17, foi encontrado um problema ao converter um componente de página em um Fragmento de experiência usando o recurso pronto para uso. Após a conversão, o fragmento de experiência parecia vazio durante a edição, apesar de ser exibido corretamente na página em que era usado. O problema resultou da criação de nó incorreto: o nó do componente foi colocado fora do nó raiz/contêiner, violando a estrutura do modelo. Você precisava mover o nó do componente manualmente para o nó raiz/contêiner correto para restaurar a capacidade de edição do fragmento. (SITES-22974)

* Depois de migrar do AEM 6.5.11 para o 6.5.20, as configurações da nuvem nos fragmentos de experiência não eram salvas corretamente. Embora as configurações parecessem ser salvas em `crx/de`, elas não seriam exibidas ao reabrir o console de configurações, indicando um problema de persistência. (SITES-22287)


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6522}

* A -->


#### Lançamentos{#sites-launches-6522}

Ao adicionar ativos de Fragmento de experiência usando o filtro de marcação na produção de AEM, o usuário pôde selecioná-lo, mas encontrou um erro ao selecionar **Criar cópia de idioma**. O comportamento esperado era que o ativo de Fragmento de experiência selecionado no filtro de marcação fosse adicionado ao projeto de tradução. (SITES-24152)

#### Verificador de links{#sites-link-checker-6522}

O LinkCheckerTask não é autenticado porque o cliente HTTP tenta NTLM antes da Autenticação Básica, fazendo com que o proxy bloqueie os usuários após várias tentativas sem êxito. Em vez disso, o sistema deve usar a Autenticação básica para autenticar no proxy, permitindo que os serviços LinkCheckerTask funcionem corretamente. (SITES-25034)


#### MSM - Live Copies{#sites-msm-live-copies-6522}

* Quando as tags de Robôs SEO são aplicadas à cópia principal e implantadas em páginas de Live Copy, os valores aparecem corretamente em `crx/de`. No entanto, os valores não eram refletidos na interface do usuário nas Propriedades da página das páginas Live Copy. (SITES-23475)
* Erros relacionados às Inicializações apareciam quando era feita uma tentativa de promover uma Inicialização por meio da interface do usuário. O assistente Promover inicialização permaneceu vazio, impedindo a conclusão do processo de promoção. (SITES-19718)
* Problemas com os Fragmentos de experiência no AEM surgiram após tentativas de criar Live Copies e realizar implantações. O problema ocorria quando usuários encontravam um erro `NotFound` ao tentar navegar de volta para a tela de gerenciamento Fragmentos de experiência da tela de Implantação. (SITES-21933)


#### Editor de página{#sites-pageeditor-6522}

* O botão Desfazer alterou a posição do componente, além de alterar o texto para a última versão. (SITES-17465)
* Quando um componente de contêiner copiado foi colado, ele aparecia visualmente duas vezes, resultando em três instâncias na página. No entanto, após a atualização da página, a duplicata desapareceu, sugerindo que o problema provavelmente era uma falha visual temporária. (SITES-21890)
* Ao navegar pelo painel esquerdo dos Componentes usando as teclas Tab ou Shift+Tab do teclado, vários elementos de texto não estavam claramente visíveis, tanto visualmente quanto no modo de tabulação. Esse problema afetava a acessibilidade, dificultando a identificação ou a interação com esses componentes durante a navegação pelo teclado. (SITES-2266)

#### Replicação{#sites-replication-6522}

No AEM 6.5.18 e 6.5.19, ao desativar uma página principal, várias solicitações de desativação foram geradas para cada página secundária. Esse problema também interrompeu o cancelamento da publicação em massa dos endpoints do GraphQL. (NPR-42075 E NPR42010)


### [!DNL Assets]{#assets-6522}

* Ao usar o recurso Connected Assets, as atualizações feitas no AEM Assets não se refletem no ambiente do AEM Sites. (ASSETS-42344)
* Problemas com o status de publicação do ativo ao mover ativos de um local para outro no Experience Manager. (ASSETS-41158)
* O upload de ativos usando a API resulta em uma mensagem de erro `unclosed resource resolver`. (ASSETS-41049)
* Problemas com a consulta de referência `AssetReferenceResolverImpl` após a atualização para o Adobe Experience Manager, Service Pack 21. (ASSETS-40384)
* No AEM versão 6.5.19, ao remover uma opção dos resultados do painel de pesquisa, também desmarca todas as outras caixas de seleção disponíveis. (ASSETS-37335)
* Valores de lixo eletrônico são exibidos na saída do Excel ao executar a operação de exportação de metadados em massa. (ASSETS-37260)
* No AEM versão 6.5.19, quando você carrega um arquivo SVG no formato UTF-8, a saída fica turva. (ASSETS-36616)
* Opção `Fetch original rendition for Dynamic Media Connected Assets` ausente na configuração do Connected Assets. (ASSETS-41726)
* As propriedades do ativo são salvas mesmo se você não definir um valor para campos obrigatórios. (ASSETS-37914)
* Se o status de processamento de um ativo for Falha ou Metadados falharam, as legendas e a interface de rastreamento de áudio não funcionam adequadamente. (ASSETS-37281)
* Quando você salva um metadado de ativo e tenta editá-lo, o nome do idioma não é exibido. (ASSETS-37281)

#### [!DNL Dynamic Media]{#assets-dm-6522}

Um problema de produção interrompeu o processo de migração quando um upload de vídeo para o Dynamic Media falhou, exibindo um erro de falha do processo na interface do usuário. (ASSETS-36038)


### [!DNL Forms]{#forms-6522}

As correções no Forms [!DNL Experience Manager] são entregues por meio de um pacote complementar separado uma semana após a data programada de lançamento do Service Pack [!DNL Experience Manager]. Nesse caso, a versão do pacote complementar do AEM 6.5.22.0 Forms está programada para quinta-feira, 28 de novembro de 2024. Uma lista de correções e aprimoramentos do Forms foi adicionada a esta seção após a versão.


<!-- #### [!DNL Adaptive Forms] {#forms-6522}

* A


#### [!DNL Forms Designer] {#forms-designer-6522}

* A -->


### Foundation {#foundation-6522}

No console do AEM Assets, ocorreu um problema ao tentar reordenar documentos DITA. A navegação estrutural na parte superior da caixa de diálogo do navegador de caminho exibe incorretamente o nome do nó, em vez do título do nó da raiz principal. O título correto do nó só é exibido depois de selecionar um item na navegação estrutural, indicando um erro de exibição temporário. (NPR-42106)


<!-- #### Apache Felix {#foundation-apachefelix-6522}


* A

#### Campaign{#foundation-campaign-6522}

* A


#### Cloud Services{#foundation-cloudservices-6522}

* A -->


#### Communities {#foundation-communities-6522}

Depois da atualização do AEM 6.5.19 para o 6.5.20, surgiu um problema em que os threads `Connection evic` não eram fechados corretamente após chamadas para `UgcSearch`. Esse problema, observado no ambiente de produção, faz com que essas threads persistam e se acumulem ao longo do tempo, possivelmente afetando o desempenho. (NPR-42019)


<!-- #### Content distribution{#foundation-content-distribution-6522}

* A -->


#### CRX {#foundation-crx-6522}

* A classificação não estava funcionando de acordo com **Grupos** no menu do lado esquerdo no Gerenciador de Pacotes do CRX. (GRANITE-53277)
* O Gerenciador de pacotes no AEM restringe a instalação de versões de pacotes inferiores por padrão, mas permite instalações forçada de versões mais antigas. No entanto, o uso da opção forçar instalação pode interferir em instalações futuras por meio do pipeline padrão. Por exemplo, se a versão 1.21 estiver instalada e a versão 1.24 for adicionada, a instalação será bem-sucedida, listando ambas as versões. No entanto, tentar instalar a versão 1.22 sobre a 1.24 falha no pipeline, mas funciona se for instalado à força, listando todas as versões. Da mesma forma, a instalação da versão 1.23 será bloqueada se a versão 1.24 já estiver presente, pois o pipeline não permite downgrades. (GRANITE-53263)


#### Granite{#foundation-granite-6522}

* Pacotes de instantâneos estavam sendo instalados no AEM usando comandos CURL. Durante a instalação, o instalador do JCR verificou os pacotes por meio do instalador do OSGI para garantir que nenhum pacote ou configuração adicional do OSGI seja necessário. Se uma versão do pacote contivesse &quot;SNAPSHOT&quot;, o instalador do OSGI acionaria o VLT para criar um pacote de instantâneo correspondente. No entanto, como cada instância do autor do AEM executa seu próprio instalador OSGI, ambas as instâncias podem tentar gerar o instantâneo simultaneamente, resultando em conflitos de sessão no repositório. (NPR-42003)
* Uma contenção de bloqueio existia em `ScriptDependencyResolver` com AEM 6.5.21. (GRANITE-53181)
* Após a atualização do AEM para 6.5.21, surgiram problemas quando caminhos relativos foram usados na sintaxe Sightly (HTL), como `data-sly-use`. (GRANITE-53080)


#### Integrações{#foundation-integrations-6522}

* Adição da declaração de atribuição legal para a interface do usuário do Cloud Service. (FORMS-16373)
* Adição de permissões de leitura para o usuário **fd-cloudservice** para acessar as configurações hCaptcha e Turnstile, permitindo que ele recupere a ID do cliente e o segredo do cliente necessários para a renderização e validação do captcha. Além disso, um modelo de Lista de controle de acesso foi implementado para gerenciar o acesso a essas configurações. (FORMS-16360)


#### Localização{#foundation-localization-6522}

Em ![Ícone de martelo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) Ferramentas > **Segurança** > ![Ícone de usuário](https://spectrum.adobe.com/static/icons/workflow_18/Smock_User_18_N.svg) **Usuários**, na página Gerenciamento de Usuários, os dados na coluna **Status** da tabela eram exibidos verticalmente. (GRANITE-48304)


<!-- #### Oak {#foundation-oak-6522}

* A -->


#### Platform{#foundation-platform-6522}

* O rastreamento do Enterprise Information Management introduzido no AEM 6.5.18 causou anomalias no cálculo das pontuações de adoção de produtos. A biblioteca de Métricas de Adobe causou esse problema ao substituir dados do usuário fornecidos pela biblioteca de rastreamento Omega. Como resultado, as pontuações de adoção para muitos clientes do AEM Sites e do AEM Assets caíram para zero a partir de fevereiro de 2024. (CQ-4358438)
* Um problema crítico foi identificado no ambiente de produção, onde o Coletor de lixo estava manipulando tags incorretamente. Especificamente, quando uma tag foi movida ou renomeada, o Coletor de Lixo falhou ao atualizar a propriedade `cq:MovedTo`, fazendo com que a tag desaparecesse das páginas. (CQ-4358293)
* Um problema com o ContextHub no AEM 6.5.19 fazia com que os segmentos resolvessem incorretamente quando um caminho de contexto era adicionado a uma instância AEM. O problema afetava especificamente o campo de URL nos objetos JavaScript gerados pelo componente página, onde o prefixo do caminho de contexto obrigatório estava ausente. Essa omissão impediu que os segmentos funcionassem como esperado. (SITES-21852)
* Atualização do AEM Quickstart para usar a biblioteca `commons-collections-3.2.2-adobe-2`. A atualização garante que o aplicativo continue funcionando sem problemas. (NPR-42150)
* A configuração do SMTP OAuth2 no AEM 6.5 difere significativamente do que é usado no AEM as a Cloud Service. Para simplificar a configuração e garantir a consistência, a configuração no AEM 6.5 precisava ser alinhada aos padrões usados no AEM as a Cloud Service. (GRANITE-53273)
* Foi encontrado um problema ao clicar em ![Ícone de bússola](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Compass_18_N.svg) > ![Ícone de projeto](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Project_18_N.svg) Projetos e, em seguida, passar o ponteiro do mouse sobre o ![Ícone à esquerda do painel](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![Ícone de divisa para baixo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg). Um acento grave foi exibido antes do texto da dica de ferramenta &quot;Somente conteúdo&quot;. (CQ-4356633)

#### Segurança{#foundation-security-6522}

* Foram encontrados problemas com uma biblioteca criptográfica JSAFE desatualizada (versão 6.0.0) no AEM. Um pacote corrigido com o JSAFE versão 6.2.5 está incluído no AEM 6.5.22. (NPR-42006)
* Ao validar os protocolos permitidos durante as verificações XSS, os manipuladores são comparados com &quot;http&quot; e &quot;https&quot;. No entanto, a propriedade `protocol` de um objeto de URL retornou esses valores com dois-pontos, como `http:` e `https:`. Essa incompatibilidade causou problemas de validação. Para garantir uma análise precisa, a verificação de protocolo é necessária para levar em conta os dois pontos ou ajustar a lógica de comparação de acordo.  (NPR-42119)
* Depois de instalar o AEM 6.5.21 (a versão anterior era AEM 6.5.19) no IBM® WebSphere® Liberty Profile e o Semeru Java 8.0, não foi possível abrir nenhuma página. Registros de erros indicavam problemas relacionados às versões de servlet que pacotes diferentes exigiam. Para resolver esse problema, a dependência em `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` teve que ser revertida porque estava relacionada ao problema. (NPR-42116)
* Vários navegadores estão eliminando o suporte aos cookies **SameSite=None**, que são usados para permitir o acesso entre sites a cookies. Como alternativa, **Cookies particionados** estão sendo introduzidos. Esses cookies isolam o armazenamento pelo contexto em que são usados, melhorando a privacidade e a segurança ao impedir o rastreamento entre sites e, ao mesmo tempo, permitir que os cookies funcionem em partições específicas, como conteúdo inserido de terceiros. (GRANITE-51953)


<!-- #### Sling{#foundation-sling-6522}

* A -->


#### Tradução{#foundation-translation-6522}

* Adição de suporte para alterações recentes nos Componentes principais às regras de tradução padrão. (NPR-42029)
* Um problema foi identificado com a exportação de arquivos XLIFF no AEM Forms. Ao usar a opção **Exportar seleção como XLIFF (somente cadeias de caracteres)**, a sequência de componentes não era mantida de forma consistente. No entanto, a sequência permanece correta ao exportar o XLIFF para um idioma específico. Dois arquivos foram fornecidos para demonstrar o problema: **DE-CH_Export.xliff** (sequência correta) e **String_Export.xliff** (sequência incorreta). (NPR-42118)


#### Interface do usuário{#foundation-ui-6522}

* O `coralui-component-dialog` estava alterando o posicionamento de `cq-dialog-actions`, possivelmente afetando o layout ou o comportamento dos botões de ação nas caixas de diálogo no AEM. (NPR-42294)
* A funcionalidade do seletor de cores no AEM estava com defeito. Quando acessada, exibia uma modal em branco, impedindo a seleção de cores. Esse problema começou após a instalação do AEM 6.5.20 no ambiente de Preparo. O seletor de cores funcionou corretamente *antes* da atualização. (NPR-42163)
* Em ![Ícone de martelo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **Ferramentas** > **Fluxo de trabalho** > **Modelos** > selecione qualquer modelo > **Iniciar fluxo de trabalho**, o ícone Procurar não estava no campo Carga da caixa de diálogo **Executar Fluxo de Trabalho**. (NPR-42162)


<!-- #### WCM{#foundation-wcm-6522}

* A


#### Workflow{#foundation-workflow-6522}

* A -->


## Instalar o [!DNL Experience Manager] 6.5.22.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.22.0 requer [!DNL Experience Manager] 6.5. Consulte a [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas. <!-- UPDATE FOR EACH NEW RELEASE -->
* O download do Service Pack está disponível na Adobe [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip).
* Em uma implantação com MongoDB e várias instâncias, instale o [!DNL Experience Manager] 6.5.22.0 em uma das instâncias do Autor usando o Gerenciador de Pacotes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> O Adobe não recomenda que você remova ou desinstale o pacote [!DNL Experience Manager] 6.5.22.0. Dessa forma, antes de instalar o pacote, você deve criar um backup do `crx-repository`, caso precise revertê-lo. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Instalar o Service Pack em [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie a instância antes da instalação se ela estiver no modo de atualização (quando a instância tiver sido atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar, faça um instantâneo ou um novo backup da instância do [!DNL Experience Manager].

1. Baixe o Service Sack de [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra o Gerenciador de Pacotes e selecione **[!UICONTROL Carregar Pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e depois selecione **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Repositório de Dados do Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Às vezes, a caixa de diálogo na interface do usuário do Gerenciador de pacotes sai durante a instalação do Service Pack. A Adobe recomenda que você aguarde a estabilização dos logs de erro antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que a instalação será bem-sucedida. Normalmente, esse problema ocorre no navegador do [!DNL Safari], mas pode ocorrer intermitentemente em qualquer navegador.

**Instalação automática**

Há dois métodos diferentes que você pode usar para instalar o [!DNL Experience Manager] 6.5.22.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote na pasta `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use a [API HTTP do Gerenciador de Pacotes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Experience Manager 6.5.22.0 não suporta a instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para trabalhar com esta versão, consulte os [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a cadeia de caracteres da versão atualizada `Adobe Experience Manager (6.5.22.0)` em [!UICONTROL Produtos Instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

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

O UberJar do [!DNL Experience Manager] 6.5.22.0 está disponível no [repositório central do Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.21/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e inclua a seguinte dependência no POM do projeto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.22</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>O UberJar e outros artefatos relacionados estão disponíveis no Repositório central Maven em vez do repositório Maven público do Adobe (`repo.adobe.com`). O arquivo UberJar principal foi renomeado para `uber-jar-<version>.jar`. Portanto, não há `classifier`, com `apis` como valor, para a tag `dependency`.


## Recursos obsoletos e removidos{#removed-deprecated-features}

Consulte [recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md/).

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

### Problema conhecido do AEM Sites {#known-issues-aem-sites-6522}

* A visualização dos fragmentos de conteúdo falha devido à proteção do DoS para uma grande árvore de fragmentos. Consulte o artigo [KB sobre as opções de configuração padrão do GraphQL Query Executor](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)


### Problemas conhecidos do AEM Forms {#known-issues-aem-forms-6522}

* Depois de instalar o AEM Forms JEE Service Pack 21 (6.5.21.0), se você encontrar entradas duplicadas de Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` na pasta `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926), execute as seguintes etapas para resolver o problema:

   1. Pare os localizadores, se eles estiverem em execução.
   1. Pare o servidor AEM.
   1. Vá para o `<AEM_Forms_Installation>/lib/caching/lib`.
   1. Remova todos os arquivos de correção Geode, exceto `geode-*-1.15.1.2.jar`. Confirme se apenas os jars Geode com `version 1.15.1.2` estão presentes.
   1. Abra o prompt de comando no modo de administrador.
   1. Instale o patch Geode usando o arquivo `geode-*-1.15.1.2.jar`.

* Se um usuário tentar visualizar um rascunho de carta com dados XML salvos, ele fica preso no estado `Loading` para algumas cartas específicas. Para baixar e instalar o hotfix, consulte o artigo [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (FORMS-14521)

* Depois de atualizar para o AEM Forms Service Pack 6.5.21.0, o serviço `PaperCapture` não executa operações de OCR (Reconhecimento Ótico de Caracteres) no PDF. O serviço não gera saída na forma de um PDF ou um arquivo de log. Para baixar e instalar o hotfix, consulte o artigo [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (CQDOC-21680)

* Quando os usuários atualizaram do AEM 6.5 Forms Service Pack 18 ou 19 para o Service Pack 20 ou 21, encontraram um erro de compilação JSP. Esse erro os impedia de abrir ou criar formulários adaptáveis. Também causou problemas com outras interfaces AEM. Essas interfaces incluíam o editor de páginas, a interface do usuário do AEM Forms, o editor de fluxo de trabalho e a interface de visão geral do sistema. (FORMS-15256)

  Se você enfrentar esse problema, execute as seguintes etapas para resolvê-lo:
   1. Navegue até o diretório `/libs/fd/aemforms/install/` no CRXDE.
   1. Exclua o pacote com o nome `com.adobe.granite.ui.commons-5.10.26.jar`.
   1. Reinicie o servidor AEM.

* Depois de atualizar para o AEM Forms Service Pack 20 (6.5.20.0) com o complemento Forms, as configurações que dependem do Adobe Analytics Cloud Service herdado usando a autenticação baseada em credencial param de funcionar. Esse problema impedia que as regras do Analytics fossem executadas corretamente. Para baixar e instalar o hotfix, consulte o artigo [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (FORMS-15428)

* Quando um usuário atualiza para o AEM Forms Service Pack 20 (6.5.20.0) no servidor JEE e gera PDF usando serviços de saída, os PDF são renderizados com problemas de acessibilidade. Para baixar e instalar o hotfix, consulte o artigo [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922112)
* Quando um usuário gera PDF com tags usando o serviço de saída no JEE, ele mostra &quot;Aviso de estrutura inadequada&quot;. Para baixar e instalar o hotfix, consulte o artigo [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922038)
* Quando um formulário é enviado no AEM Forms JEE, as instâncias de um elemento XML repetido são removidas dos dados. Para baixar e instalar o hotfix, consulte o artigo [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922017)
* Quando um usuário em um ambiente Linux® renderiza um formulário adaptável (no JEE) no HTML, ele não é renderizado corretamente. Para baixar e instalar o hotfix, consulte o artigo [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921957)
* Quando um usuário converte um arquivo XTG no formato PostScript usando o Serviço de Saída no AEM Forms JEE, ocorre uma falha com o erro: `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`. Para baixar e instalar o hotfix, consulte o artigo [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921720)
* Depois de atualizar para o AEM Forms Service Pack 18 (6.5.18.0) no servidor JEE, quando um usuário envia um formulário, ele falha ao renderizar HTML5 ou PDF forms e falhas XMLFM. Para baixar e instalar o hotfix, consulte o artigo [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921718)
* Na Visualização de impressão da interface do usuário do Agente de comunicações interativas, o símbolo de moeda (como cifrão $) é exibido de forma inconsistente para todos os valores do campo. Aparece para valores até 999, mas está ausente para valores de 1000 e superiores. (FORMS-16557)
* Quaisquer modificações no XDP de fragmentos de layout aninhados em uma comunicação interativa não são refletidas no editor IC. (FORMS-16575)
* Na Visualização de impressão da interface do usuário do Agente de comunicações interativas, alguns valores calculados não são exibidos corretamente. (FORMS-16603)
* Quando a carta é exibida na Visualização de impressão, o conteúdo é alterado. Ou seja, alguns espaços desaparecem e determinadas letras são substituídas por &quot;x&quot; (FORMS-15681)

## Pacotes OSGi e pacotes de conteúdo incluídos{#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de Conteúdo incluídos nesta versão do Service Pack do [!DNL Experience Manager] 6.5:

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.22.0](/help/release-notes/assets/65220-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de Pacotes de Conteúdo incluídos no Experience Manager 6.5.22.0](/help/release-notes/assets/65220-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites restritos{#restricted-sites}

Esses sites só estão disponíveis para clientes do. Se você for um cliente do e precisar de acesso, entre em contato com o gerente de conta da Adobe.

* [Download do produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Contate o Suporte ao Cliente do Adobe](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/br/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação do 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Inscrever-se para obter atualizações de produtos de prioridade Adobe](https://www.adobe.com/subscription/priority-product-update.html)
