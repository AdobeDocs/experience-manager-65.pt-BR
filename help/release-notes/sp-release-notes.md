---
title: '[!DNL Experience Manager] Notas de versão do service pack 6.5'
description: Notas de versão específicas do  [!DNL Adobe Experience Manager] 6.5 service pack 9
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 19dd081674b4954498d6aa62335f6b5a9f2a4146
workflow-type: tm+mt
source-wordcount: '3835'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] Notas de versão do service pack 6.5 {#aem-service-pack-release-notes}

## Informações da versão {#release-information}

| Produtos | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.9.0 |
| Tipo | Lançamento do Service Pack |
| Data | 27 de maio de 2021 |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9-1.0.zip) |

## O que está incluído em [!DNL Adobe Experience Manager] 6.5.9.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] A versão 6.5.9.0 inclui novos recursos, principais melhorias solicitadas pelo cliente e melhorias de desempenho, estabilidade e segurança, lançadas desde a disponibilização da versão 6.5 em abril de 2019. O service pack é instalado em [!DNL Adobe Experience Manager] 6.5.

Os principais recursos e aprimoramentos introduzidos no [!DNL Adobe Experience Manager] 6.5.9.0 são:

* [!DNL Experience Manager Sites] O componente Dynamic Media Foundation agora permite ativar ou desativar a otimização para dispositivos de resolução mais alta ao usar uma predefinição de imagem responsiva ou Recorte inteligente.

* Para melhorar o desempenho, a condição `hidden=false` é movida da consulta JCR para o avaliador [!UICONTROL QueryBuilder]. Para verificar se um predicado oculto está funcionando após a alteração, [!DNL Experience Manager] verifica se qualquer pasta oculta não é exibida.

* Capacidade de restaurar páginas e árvore excluídas em uma página [!DNL Experience Manager Sites].

* Suporte para um novo usuário atualizar o token de acesso usando um token de atualização para o serviço de configuração do remetente.

* [Suporte ao mecanismo SMTP XOAUTH2](/help/sites-administering/notification.md#setting-up-oauth) para o serviço de configuração de email.

* Suporte para [!DNL MongoDB] versões 4.2 e 4.4.

* Ocorrências de nomes relacionados a Hong Kong, Macau e Taiwan são atualizadas de acordo com as novas convenções de nomenclatura para localidades e regiões chinesas.

* Aprimoramentos de acessibilidade em [!DNL Experience Manager] [[!DNL Assets]](#assets-accessibility-6590) e [[!DNL Dynamic Media]](#accessibility-dm-6590).

* O Smart Imaging DPR (Device Pixel Ratio) e a otimização da largura de banda da rede permitem fornecer imagens de melhor qualidade com eficiência; em dispositivos com telas de alta resolução e largura de banda de rede restrita. Para obter detalhes e a linha do tempo, consulte [perguntas frequentes sobre a geração inteligente de imagens](/help/assets/imaging-faq.md).

* [!DNL Dynamic Media] delivery (modificador de `fmt` URL) suporta o formato de imagem de próxima geração AVIF (formato AV1 Image ). Para obter mais detalhes e linha do tempo, consulte [image service and rendering API fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html).

* Capacidade de enviar um email de notificação para um grupo usando a etapa do fluxo de trabalho [!UICONTROL Atribuir tarefa] .

* Capacidade de recuperar um rascunho de Comunicação Interativa após modificar a Comunicação Interativa de origem.

* Defina o nome de domínio personalizado para carregar, renderizar e validar o serviço reCAPTCHA em [!DNL Experience Manager Forms].

* Aprimoramentos de dados de entrada para [!UICONTROL Invoke Form Data Model Service] etapa do fluxo de trabalho.

* Capacidade de usar várias páginas principais em um modelo de Documento de registro em [!DNL Experience Manager Forms].

* A página de suporte é interrompida no Documento de registro em [!DNL Experience Manager Forms].

* O repositório integrado (Apache Jackrabbit Oak) foi atualizado para 1.22.7.

Para obter uma lista completa dos recursos e aprimoramentos introduzidos no [!DNL Experience Manager] 6.5.9.0, consulte [novidades no [!DNL Adobe Experience Manager] 6.5 Service Pack 9](new-features-latest-service-pack.md).

>[!NOTE]
>
>A partir do Service Pack 9, [!DNL Experience Manager] os clientes podem desenvolver e operar seus aplicativos [!DNL Experience Manager] com distribuições dos [!DNL Azul Zulu] builds of OpenJDK, compatíveis com padrões do Java™ SE.
>O suporte para [!DNL Azul Zulu] JDKs também é fornecido pelo Adobe aos clientes [!DNL Experience Manager].
>Você pode baixar as versões relevantes dos JDKs [!DNL Azul Zulu] de [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
>Os direitos de uso da tecnologia Oracle Java™, conforme distribuída pela Adobe, expirarão no final de dezembro de 2022. [!DNL Experience Manager] os clientes do são incentivados a planejar e implementar o uso dos  [!DNL Azul Zulu] JDKs mais recentes até essa data. Para obter mais informações sobre o uso da tecnologia [!DNL Oracle Java™] e da tecnologia [!DNL Azul Zulu], consulte as [Perguntas frequentes](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf) associadas.

Esta é a lista de correções fornecidas na versão [!DNL Experience Manager] 6.5.9.0.

### [!DNL Sites] {#sites-6590}

* As páginas publicadas com a propriedade Requisito de autenticação ativada não redirecionam para a página de logon e retornam a mensagem de erro 404 (NPR-36354).

* Ao criar um hiperlink, a opção para pesquisar um link não funciona no componente de texto (NPR-35849).

* Uma consulta transversal é acionada ao usar a API `com.day.cq.wcm.commons.ReferenceSearch`. Isso afeta o desempenho do servidor [!DNL Experience Manager] (NPR-36407).

* O contêiner de layout aninhado dentro de outro contêiner de layout redimensionado mostra um número incorreto de colunas para seus componentes filhos, resultando em esses componentes não serem alinhados à grade (NPR-36359).

* O Linkchecker externo exibe links externos válidos como links inválidos (NPR-36289).

* Depois de exibir referências por algum tempo, o painel de referências começa a mostrar uma mensagem de erro (NPR-36167).

* Ao mover um componente, o parsys criado automaticamente não tem o nó `sling:resourceType` (NPR-36165).

* Ao tentar sincronizar uma live-copy (ao usar configurações de implantação [!UICONTROL Ativar na ativação do Blueprint] e [!UICONTROL Desativar na ativação do Blueprint]) se um componente for excluído na livecopy principal, a sincronização falhará e um `NullPointerException` será registrado (NPR-36127).

* Quando um usuário digita o texto improvisado para a tag (tag que não existe no sistema) e pressiona Enter, a tag aparece sob o campo, mas quando o Fragmento de conteúdo é salvo e reaberto, a tag improvisada desaparece (NPR-36132).

* A Caixa de entrada não tem a opção de exibir o status de Operações assíncronas (NPR-36104).

* Um componente duplicado é criado após a restauração da herança (NPR-36000).

* Ao usar o `RemoteContentRenderingService`, a solicitação para o `RemoteContentRendererRequestHandler.getRequest` sempre inclui a página raiz para o `ComponentExporter`, mas não inclui a página solicitada se não estiver incluída no modelo raiz com base na profundidade de passagem e no conjunto de opções de filtragem. A solicitação sempre deve incluir a página solicitada para que o SPA tenha informações suficientes para renderizar uma resposta (NPR-35961).

* Os itens onTime/offTime não ativam/desativam no onTime/offTime esperado (NPR-35936).

* Ao publicar uma página contendo um Fragmento de experiência que não tem propriedade `cq:lastModified`, ocorre um `NullPointerException` (NPR-35914).

* Ao tentar redimensionar um componente dentro de um contêiner, não é possível redimensionar de volta ao tamanho original. Quando o tamanho do contêiner do componente é reduzido, não é possível definir o tamanho de volta para o original (NPR-35809).

* Na caixa de diálogo de implantação, acionada no editor ou na Visão geral da Live Copy, os ícones de status para páginas desanexadas, suspensas ou não criadas estão incorretos (NPR-35691).

* A implementação das propriedades na página do Multi-Site Manager de página principal ignora a página de implantação e a caixa de seleção de subpáginas (NPR-35634).

* A funcionalidade de árvore de restauração, disponível na interface clássica, está ausente da interface do usuário de toque (CQ-4315352, CQ-4309415).

* Problemas ao reverter a herança e ao rolar a página em uma página [!DNL Experience Manager Sites] (NPR-36033).

### [!DNL Assets] {#assets-6590}

Os seguintes aprimoramentos na experiência do usuário são feitos em [!DNL Assets]:

* Para exibir ativos não classificados com base em qualquer um dos parâmetros [!UICONTROL Create], [!UICONTROL Modify] ou [!UICONTROL Name], [!DNL Adobe Experience Manager] oferece uma opção [!UICONTROL None] dentro das opções [!UICONTROL Sort by]. A opção [!UICONTROL None] garante que os ativos na interface do usuário do Assets (na exibição Cartão, Coluna e Insights) estejam na mesma ordem em que existem no nó JCR (NPR-36356).

* Para tornar a ID de email em minúsculas na resposta da API ACP de [!DNL Adobe Experience Manager] uma configuração opcional é introduzida; como os usuários [!DNL Adobe Asset Link] não poderiam fazer check-in de ativos se a ID não tivesse todos os caracteres em minúsculas. O painel [!DNL Adobe Asset Link] consome a resposta da API ACP de [!DNL Adobe Experience Manager] (CQ-4317704).

[!DNL Adobe Experience Manager] A versão 6.5.9.0  [!DNL Assets] oferece as seguintes melhorias de acessibilidade.

O contraste (com o plano de fundo) do texto e dos ícones a seguir é aprimorado para que os usuários com visão e percepção de cor limitadas possam compreender:

* Título do ativo na página [!UICONTROL Propriedades] (NPR-35967).
* Ícones de classificação de estrelas nas seções [!UICONTROL Classificação] em vários lugares (NPR-36009).
* Texto na exibição de ativo e pasta Cartão (NPR-35966).
* Texto do espaço reservado na exibição [!UICONTROL Linha do tempo] (NPR-35965).
* Nomes de ativos nos resultados da pesquisa de ativos (NPR-35964).
* Texto de espaço reservado na caixa de diálogo [!UICONTROL Compartilhamento de link] (NPR-35963).
* [!UICONTROL Metadados],  [!UICONTROL Status] e   Outro texto na opção   Listagem na caixa de diálogo  [!UICONTROL Exibir ] configurações (NPR-35910).
*  Localização e  [!UICONTROL tipo para texto de espaço reservado para ] pesquisa na pesquisa global (NPR-35909).
* Expanda e recolha os ícones em [!UICONTROL Árvore de conteúdo] (NPR-35908).
* O texto [!UICONTROL Assets] na página em que as pastas de ativos são exibidas (NPR-35905).
* Texto em [!UICONTROL Metadados do ativo], [!UICONTROL Estatísticas de uso] na opção [!UICONTROL Visão geral] na página Detalhes do ativo (NPR-35904).
* Texto para teclas de atalho para as opções [!UICONTROL properties] e [!UICONTROL edit] na página Detalhes do ativo (NPR-35904).

[!DNL Adobe Experience Manager] A versão 6.5.9.0  [!DNL Assets] corrige os seguintes problemas.

* As tags criadas a partir de um elemento de seleção de tag em um formulário [!UICONTROL Folder Metadata Schema] não são salvas (NPR-36119).

* Quando uma pequena elipse é usada para anotar ativos, a elipse se sobrepõe ao número da anotação na versão impressa (NPR-36114).

* Às vezes, na exibição em Coluna, [!DNL Experience Manager] não solicita conflito de ativos duplicados quando um ativo duplicado é carregado (NPR-36048).

* A caixa de diálogo Compartilhar link não é fechada clicando no botão Fechar se ele estiver aberto e nenhuma alteração for feita (NPR-36030).

* Quando vários ativos são selecionados para atualizar as propriedades, às vezes ocorre um erro ou as propriedades de um ativo desmarcado são atualizadas (NPR-36002).

* Quando os espaços em branco de upload de ativos são adicionados no início ou no fim dos nomes de arquivos de ativos, com os caracteres restantes iguais ao nome de um ativo existente no repositório, o ativo existente é substituído sem registrar nenhum erro (NPR-36001).

* Quando o vídeo é reproduzido na página de detalhes do ativo, as opções de reprodução e pausa não funcionam (NPR-35999).

* Ao cancelar a publicação de ativos em massa, o Brand Portal gera um erro sugerindo que o URI da solicitação é muito longo (NPR-35954).

* Quando um ativo com texto de anotação longo é impresso, o texto da anotação é cortado, mesmo se espaço estiver disponível (NPR-35948).

* A opção para mover para a Próxima página está desativada ao selecionar a página na exibição Modelos selecionada na página Criar catálogo (CQ-4315462).

* Quando o fluxo de trabalho de atualização do ativo é iniciado no ativo de vídeo, a página é atualizada repetidamente (CQ-4313375).

* As pastas DAM não podem ser excluídas ou movidas, e uma exceção é registrada (NPR-35942).

### [!DNL Dynamic Media] {#dynamic-media-6590}

[!DNL Adobe Experience Manager] A versão 6.5.9.0  [!DNL Assets] oferece as seguintes melhorias de acessibilidade em  [!DNL Dynamic Media].

* Ao abrir a caixa de diálogo para adicionar ativos usando teclas do teclado no editor [!UICONTROL Conjunto de imagens]:
   * Os leitores de tela registram que a caixa de diálogo está aberta.
   * O foco do teclado é movido para a caixa de diálogo quando ele é aberto.
   * O foco do teclado volta para a opção Adicionar ativo quando a caixa de diálogo é fechada (CQ-4312134).

* Agora é possível adicionar e editar Pontos de acesso em ativos usando teclas de teclado no editor de ponto de acesso (CQ-4305965).

* Agora você pode colocar hiperlink no ponto de acesso por meio do gerenciamento de pontos de acesso usando teclas do teclado. O foco do leitor de tela agora é movido para o campo para editar Caminho do URL e a opção para Abrir caixa de diálogo de seleção (CQ-4290735).

* O contraste (com fundo) do texto e os controles na página Editor do conjunto de imagens são aprimorados, para que os usuários com visão e percepção de cor limitadas possam ser compreendidos (CQ-4290733).

* Agora é possível navegar até as opções de compartilhamento de ativos no Editor de predefinições do visualizador e recolher a opção de compartilhamento expandida usando teclas de teclado (CQ-4290724).

* Agora é possível navegar e exibir dicas de ferramentas nos ícones de informações e de alerta nas guias Básico e Avançado da página Editar codificação de vídeo usando as teclas do teclado (CQ-4290722).

* Os leitores de tela agora narram as instruções para vários campos na guia Aparência e na guia Comportamento no Editor de predefinições do visualizador (CQ-4290721).

* Ao navegar pela página Editar predefinição de imagem no modo Formulário , o leitor de tela narra a finalidade e os nomes de vários campos e controles (CQ-4290717).

* Ao navegar na página de detalhes de ativos, os leitores de tela agora descrevem a finalidade de várias opções em Visualizadores (CQ-4290716).

* O contraste (com o plano de fundo) do texto de espaço reservado Todas as representações na opção Representações da página de detalhes do ativo é aprimorado, para que os usuários com visão limitada e percepção de cor possam compreender (CQ-4290713).

* O asterisco visual para indicar o campo obrigatório agora é fornecido no campo Título do ativo no Editor do conjunto de imagens, e os leitores de tela anunciam as informações necessárias para o campo (CQ-4290712).

* Agora, os leitores de tela podem acessar e registrar a finalidade de várias opções interativas nos Visualizadores na página Detalhes do ativo (CQ-4290708).

Os ativos Adobe Experience Manager 6.5.9.0 corrigem os seguintes problemas em [!DNL Dynamic Media]:

* O Custom ViewerPresets e o CSS não são replicados para [!DNL Dynamic Media] quando [!DNL Dynamic Media] é ativado seletivamente e desativado por [default](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html#troubleshoot-dm-config) (NPR-36232).

* Ao tentar visualizar representações de vídeo na página de detalhes do ativo, os vídeos são lentos e carregados (CQ-4320122).

* A página do navegador não responde e fica lenta ao fazer upload de mais de 200 ativos com o Detector de ativos duplicados ativado (CQ-4319633).

* Quando um ativo de imagem panorâmica é adicionado ao componente de mídia panorâmica em uma página, um erro de referência não captada é registrado (CQ-4317666).

* Quando o visualizador de mídia interativa é implementado com o Fragmento de experiência, o Fragmento de experiência não é aberto no publicador e um erro é registrado (CQ-4317655).

* [!UICONTROL A opção Publicar no Dynamic ] Media não está disponível nas opções  [!UICONTROL de ] Publicação rápida em   Properties (CQ-4317199).

* Os autores do site com permissões somente leitura podem usar a funcionalidade de recorte inteligente em ativos e editar as representações recortadas inteligentes (CQ-4316450).

* As anotações de vídeo não funcionam para caminhos de pastas onde a configuração [!DNL Dynamic Media] não está ativada, mesmo se a instância [!DNL Experience Manager] estiver configurada no modo [!DNL Dynamic Media] (CQ-4314950).

* Quando o título do ativo tem caracteres de byte duplo, byte múltiplo, ASCII alto, cirílico, par substituto, hebraico, árabe e GB18030, em seguida, ao publicar no Dynamic Media o título do ativo tem um ponto de interrogação (?) (CQ-4311872).

>Problemas conhecidos de reprodução de vídeo no Dynamic Media *somente no Experience Manager 6.5.9.0*:
>
>* 

   <!-- CQDOC-18116 -->You cannot play video renditions from the asset's Details page on Experience Manager - Dynamic Media running in hybrid mode.
>* 

   <!-- CQDOC-18116 -->You cannot stream videos on Experience Manager - Dynamic Media running in hybrid mode.


### Plataforma {#platform-6590}

* Ao gerar uma miniatura para um blueprint e implantar as alterações na live copy, a herança de alguns campos não funciona (CQ-4319517).

* Ao criar uma pasta, selecione a propriedade Orderable e adicione mais de 20 ativos à pasta, selecionar todos os ativos na pasta exibe uma contagem incorreta (CQ-4316243).

* Quando você atualiza uma página, a classificação de pastas ou ativos não exibe os resultados apropriados (CQ-4316200).

* A biblioteca JavaScript do Handlebars é atualizada ao v4.7.7 (NPR-36375).

* Pacotes personalizados não são atualizados ao instalar um novo pacote de código usando o Gerenciador de pacotes (NPR-35949).

* Um pacote `resourceresolver` Sling está causando falha na consulta `Sling:alias` (NPR-35335).

* O caminho do contexto é removido ao configurar o SSL no Experience Manager (NPR-35294).

* A exceção `SegmentNotFound` é retornada após uma sessão de longa duração (NPR-36405).

### Integrações {#integrations-6590}

* Não é possível salvar as propriedades da página com a herança ativada para Fragmentos de experiência do Cloud Services (NPR-36107).

* A paginação da interface do usuário IMS e o carregamento lento não exibem os resultados apropriados (NPR-36046).

* Ao criar a configuração do A4T do Target e selecionar a fonte de relatórios como [!DNL Adobe Analytics], não há conjuntos de relatórios habilitados para Adobe Target disponíveis na lista suspensa (NPR-36006).

### Projetos {#projects-6590}

* Não é possível salvar as propriedades de um projeto, pois o caminho JCR para o projeto não foi resolvido devido a uma barra (`/`) extra anexada ao caminho do projeto (NPR-36191).

### Screens {#screens-6590}

* [!DNL Experience Manager Screens] os players não podem autenticar se um manipulador de autenticação de dois fatores personalizado for usado (NPR-35854).

### Commerce {#commerce-6590}

* O assistente [!UICONTROL Commerce Catalog] falha ao carregar mais de 40 itens na exibição em Coluna (CQ-4318379).

### Projetos de tradução {#translation-6590}

* As opções Atualizar ou Substituir não são exibidas durante a retradução de uma página `es` para `es_es` (NPR-36170).

* Quando a opção de aprovação automática é selecionada para um projeto com tradução humana, o status da tarefa é exibido como `Unknown` (NPR-35981).

* Quando você está traduzindo uma página, o caminho de referência [!DNL Experience Fragments] não é atualizado para o caminho de referência [!DNL Experience Fragment] de destino (NPR-35911).

* Ao fazer alterações nas páginas pai e filho e enviar a página pai para tradução, as páginas filho também são traduzidas incorretamente (NPR-35896).

* Quando há vários projetos de tradução simultâneos para uma página selecionada, a opção [!UICONTROL Ir para projetos] não vincula ao projeto de tradução mais recente (NPR-35454).

* Ao publicar ativos em [!DNL Dynamic Media], [!DNL Experience Manager] exibe uma mensagem incorreta para tags não publicadas (CQ-4315914, CQ-4315913).

* Quando você abre um trabalho excluído, [!DNL Experience Manager] exibe uma mensagem incorreta (CQ-4315910).

### Fluxo de trabalho {#workflow-6590}

* Quando você clica nas ações Concluir, Delegar ou Abrir para os itens disponíveis na Caixa de entrada, não há pista visual para a conclusão dessas ações (NPR-36317).

### [!DNL Communities] {#communities-6590}

* Na filtragem de spam, o sistema consome 100% do espaço de heap Java™, tornando o servidor Experience Manager não responsivo (NPR-36316, NPR-36493).
* Nos fóruns, os dados das sessões do JCR originados de `SearchCommentSocialComponentListProvider` vazam (NPR-36235).
* Abrir uma mensagem de caixa de entrada específica reflete todas as mensagens com paginação inadequada e outros problemas (NPR-35917).

### [!DNL Brand Portal] {#brandportal-6590}

* O sinalizador de recurso de origem de ativos é habilitado automaticamente ao configurar [!DNL Experience Manager Assets] com [!DNL Brand Portal] (NPR-36010).

### [!DNL Forms] {#forms-6590}

>[!NOTE]
>
>* O [!DNL Experience Manager Forms] lança os pacotes complementares uma semana após a data programada de lançamento do [!DNL Experience Manager] Service Pack.
>* Agora você pode desenvolver e operar aplicativos com [!DNL Azul Zulu] criações de [!DNL OpenJDK] para [!DNL Experience Manager Forms] em implantações OSGi.


**Formulários adaptáveis**

* Problemas de inicialização de idioma em [!DNL Experience Manager Forms] 6.5.7.0 ao gerar vários dicionários de tradução (NPR-36439).
* Ao adicionar um anexo ao fragmento de formulário adaptável e enviar o formulário, [!DNL Experience Manager Forms] exibe a seguinte mensagem de erro (NPR-36195):

   ```TXT
    POST /content/forms/af/attachmentissue/jcr:content/guideContainer.af.submit.jsp HTTP/1.1] com.adobe.aemds.guide.servlet.GuideSubmitServlet [AF] Invalid file name or mime type for file resulted in submission failure
   ```

* Quando você usa a tradução humana para atualizar um dicionário e, em seguida, visualizar um formulário adaptável, as modificações não são exibidas (NPR-36035).

**Comunicações interativas**

* Ao fazer upload de uma imagem usando o canal de Impressão de Comunicações interativas e editá-la, a imagem não estará mais visível (NPR-36518).

* Ao editar um ativo de texto e preencher um espaço reservado, todos os elementos interativos são removidos do painel de navegação (NPR-35991).

**Fluxo de trabalho**

* Quando você chama o terminal REST de um serviço [!DNL Experience Manager Forms] no JBoss®, [!DNL Experience Manager] exibe a seguinte mensagem de erro (NPR-36305):

   ```TXT
   Invalid input. The maximum length of 2000 characters was exceeded.
   ```

**BackendIntegration**

* Não é possível salvar um modelo de dados de formulário ao vincular o argumento de serviço de Leitura a um valor literal que contém um traço (NPR-36366).

**Segurança de documentos**

* Ao definir a certificação e o HSM para GlobalSign, [!DNL Experience Manager Forms] exibe as mensagens de erro `Unsuported Algorithm` e `Invalid TSA Certificate` ao adicionar um carimbo de data e hora ao LTV (NPR-36026, NPR-36025).

**Serviços de documento**

* Atualizações da biblioteca [!DNL Gibson] para integração com [!DNL Experience Manager Forms] (NPR-36211).

**Foundation JEE**

* Quando você seleciona Gerenciamento de ponto de extremidade na interface do usuário do administrador, [!DNL Experience Manager Forms] exibe a mensagem de erro `endpoint registry failure` (CQ-4320249).

Para obter informações sobre atualizações de segurança, consulte a [[!DNL Experience Manager] página de marcadores de segurança](https://helpx.adobe.com/security/products/experience-manager.html).

## Instalar 6.5.9.0 {#install}

**Requisitos de configuração e mais informações**

* O Experience Manager 6.5.9.0 requer o Experience Manager 6.5. Consulte a [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas.
* O download do service pack está disponível no Adobe [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Em uma implantação com MongoDB e várias instâncias, instale o Experience Manager 6.5.9.0 em uma das instâncias do autor usando o Gerenciador de pacotes.

>[!NOTE]
>
>O Adobe não recomenda remover ou desinstalar o pacote [!DNL Adobe Experience Manager] 6.5.9.0.

### Instalar o service pack {#install-service-pack}

Para instalar o service pack em uma instância [!DNL Adobe Experience Manager] 6.5, siga estas etapas:

1. Reinicie a instância antes da instalação se a instância estiver no modo de atualização (e esse é o caso quando a instância foi atualizada de uma versão anterior). O Adobe também recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar, faça um instantâneo ou um novo backup da sua instância [!DNL Experience Manager].

1. Baixe o service pack de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9-1.0.zip).

1. Abra Gerenciador de pacotes e clique em **[!UICONTROL Fazer upload de pacote]** para fazer upload do pacote. Para saber mais, consulte [Gerenciador de Pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>A caixa de diálogo na interface do usuário do Gerenciador de Pacotes às vezes sai durante a instalação do service pack. O Adobe recomenda que você aguarde a estabilização dos registros de erros antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações foram bem-sucedidas. Normalmente, isso acontece em [!DNL Safari], mas pode acontecer intermitentemente em qualquer navegador.

**Instalação automática**

Há duas maneiras de instalar automaticamente [!DNL Experience Manager] 6.5.9.0 em uma instância de trabalho:

A. Coloque o pacote na pasta `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é instalado automaticamente.

B. Use a API HTTP [do Gerenciador de Pacotes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Adobe Experience Manager 6.5.9.0 não suporta a instalação do Bootstrap.

**Validar a instalação**

1. A página de informações do produto (`/system/console/productinfo`) exibe a cadeia de caracteres de versão atualizada `Adobe Experience Manager (6.5.9.0)` em [!UICONTROL Produtos instalados].

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
>O Experience Manager 6.5.9.0 inclui uma nova versão do [Pacote de Compatibilidade AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). Se você estiver usando uma versão mais antiga do Pacote de Compatibilidade do AEM Forms e estiver atualizando para o Experience Manager 6.5.9.0, instale a versão mais recente do pacote após a instalação do Pacote de Suplementos do Forms.

### Instalar o Adobe Experience Manager Forms no JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Pule se você não estiver usando o AEM Forms no JEE. As correções no Adobe Experience Manager Forms no JEE são entregues por meio de um instalador separado.

Para obter informações sobre como instalar o instalador cumulativo do Experience Manager Forms no JEE e na configuração pós-implantação, consulte as [notas de versão](jee-patch-installer-65.md).

>[!NOTE]
>
>Depois de instalar o instalador cumulativo do Experience Manager Forms no JEE, instale o pacote complementar mais recente do Forms, exclua o pacote do complemento Forms da pasta `crx-repository\install` e reinicie o servidor.

### UberJar {#uber-jar}

O UberJar para Experience Manager 6.5.9.0 está disponível no [Repositório Central Maven](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.9-1.0/).

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e inclua a seguinte dependência no POM do projeto:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.9-1.0</version>
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
| Integrações | A tela de aceitação **[!UICONTROL AEM Cloud Services]** está obsoleta. Com a integração do Experience Manager e do Adobe Target atualizada no Experience Manager 6.5 para oferecer suporte à API do Adobe Target Standard, que usa autenticação via Adobe IMS e [!DNL Adobe I/O], e com a função crescente do Adobe Launch para instrumentar páginas Experience Manager para análise e personalização, o assistente de aceitação se tornou funcionalmente irrelevante. | Configure conexões do sistema, autenticação Adobe IMS e [!DNL Adobe I/O] integrações por meio dos respectivos serviços em nuvem [!DNL Experience Manager]. |
| Conectores | O Conector Adobe JCR para Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 está obsoleto para o Experience Manager 6.5. | N/A |

## Problemas conhecidos {#known-issues}

* Se estiver atualizando sua instância [!DNL Experience Manager] da versão 6.5 para a 6.5.9.0, você poderá visualizar as exceções `RRD4JReporter` no arquivo `error.log`. Reinicie a instância para resolver o problema.

* Se você instalar o [!DNL Experience Manager] 6.5 Service Pack 5 ou um service pack anterior no [!DNL Experience Manager] 6.5, a cópia em tempo de execução do modelo de fluxo de trabalho personalizado de ativos (criado em `/var/workflow/models/dam`) será excluída.
Para recuperar a cópia de tempo de execução, o Adobe recomenda sincronizar a cópia de tempo de design do modelo de fluxo de trabalho personalizado com a cópia de tempo de execução usando a API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Se uma pasta na hierarquia for renomeada em [!DNL Assets] e uma pasta aninhada contendo um ativo for publicada em [!DNL Brand Portal], o título da pasta não será atualizado em [!DNL Brand Portal] até que a pasta raiz seja republicada.

* Quando um usuário seleciona configurar um campo pela primeira vez em um formulário adaptável, a opção para salvar uma configuração não é exibida no Navegador de propriedades. Selecionar para configurar outro campo do formulário adaptável no mesmo editor resolve o problema.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação do Experience Manager 6.5.x.x:
   * &quot;Quando a integração do Adobe Target é configurada no Experience Manager usando a API do Target Standard (autenticação IMS), a exportação dos Fragmentos de experiência para o Target resulta na criação de tipos de ofertas incorretos. Em vez do tipo &quot;Fragmento de experiência&quot;/fonte &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/fonte &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * A validação do lado do servidor do Adaptive Form falha quando funções agregadas, como SUM, MAX e MIN são usadas (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de Banner de compra.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tempo limite aguardando a conclusão da alteração de reg não registrada.

## Pacotes de conteúdo e pacotes OSGi incluídos {#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos em [!DNL Experience Manager] 6.5.9.0:

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.9.0](assets/6590_bundles.txt)

* [Lista de pacotes de conteúdo incluídos na Experience Manager 6.5.9.0](assets/6590_packages.txt)

## Sites restritos {#restricted-sites}

Esses sites só estão disponíveis para clientes do . Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* Consulte [como entrar em contato com o Atendimento ao Cliente do Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Notas de versão 6.5](/help/release-notes/release-notes.md)
* [[!DNL Experience Manager] página do produto](https://www.adobe.com/br/marketing/experience-manager.html)
* [[!DNL Experience Manager] Documentação 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR)
* [Inscreva-se em Atualizações de produtos de prioridade da Adobe](https://www.adobe.com/subscription/priority-product-update.html)

