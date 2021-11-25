---
title: Novidades do [!DNL Experience Manager] 6.5 Service Pack 11
description: Novidades do [!DNL Experience Manager] 6.5 Service Pack 11
contentOwner: AK
mini-toc-levels: 1
exl-id: 32470e6e-8a66-4670-82da-2259f6e001c3
source-git-commit: 35260325b583bd047f22ffa88afb9469b2023e60
workflow-type: tm+mt
source-wordcount: '4391'
ht-degree: 1%

---

# Novidades do [!DNL Adobe Experience Manager] 6.5 Service Pack 11 {#aem-whats-new-service-pack}

<!-- TBD: Downsample this image. We do not need as big an image since customers don't use as big a screen to view. Also, having a 700+ KB decorative image is bad for page load time.
-->

![Novidades](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 Os Service Packs oferecem novos recursos, melhorias solicitadas pelo cliente e melhorias de desempenho, estabilidade e segurança em intervalos trimestrais. A disponibilidade trimestral facilita o acesso e a adoção de novos recursos e inovações.

Este artigo destaca os recursos incluídos no Service Pack mais recente [principais recursos incluídos nos 6.5 Service Packs anteriores](#key-features-previous-service-packs)e o [versões principais desde o último Service Pack](#key-releases-since-last-sp) versão.

## [!DNL Adobe Experience Manager Sites] {#aem-sites}

* A geração automática de mapa de site para fins de SEO é possível usando o [Pacote de índice SEO](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip). Ele é compatível com mapas de site, URLs alternativos, metatags de robô e muito mais na [!DNL Core Components].

* Adição de suporte a vários campos para o tipo de dados de texto multilinha.

* Aprimoramento para tornar os usuários conscientes do trabalho assíncrono em execução no momento em segundo plano, para evitar que ele acione várias operações assíncronas no mesmo caminho.

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* As melhorias na experiência do usuário exibem o número de ativos presentes em uma pasta. Para mais de 1000 ativos em uma pasta, [!DNL Assets] exibe 1000+.

   ![Número de ativos em uma pasta](/help/assets/assets/browse-folder-number-of-assets.png)

* Os seguintes aprimoramentos de acessibilidade estão disponíveis:

   * Na exibição de cartão na [!DNL Assets] repositório, ao usar `Tab` para mover o foco para o primeiro item que abre Ações rápidas em foco, o leitor de tela anuncia o nome do item focado.
   * Em [!DNL Dynamic Media] [!UICONTROL Editor de predefinições do visualizador], quando a Cor da sombra e a Cor da borda não estão presentes, as entradas são desativadas usando a propriedade disabled . Os usuários de teclado não conseguem focalizar a entrada e os leitores de tela não anunciam o estado do controle como desativado.
   * Em [!DNL Dynamic Media], na interface do para criar um novo perfil de codificação de vídeo, a variável [!UICONTROL Proporção de corte inteligente] está rotulada para acessibilidade, de modo que os leitores de tela a anunciem adequadamente.

### [!DNL Dynamic Media] {#dynamic-media}

* Agora você pode usar [!DNL Dynamic Media] para configurar as Configurações gerais em vez de precisar passar pelo [!DNL Dynamic Media Classic] aplicativo de desktop. Consulte [Definir as configurações gerais do Dynamic Media](/help/assets/dm-general-settings.md).

   ![Configurações gerais do DM](/help/assets/assets-dm/dm-general-settings.png)

* Agora você pode usar [!DNL Dynamic Media] para configurar a Configuração de publicação em vez de precisar passar pelo [!DNL Dynamic Media Classic] aplicativo de desktop. Consulte [Configurar a publicação do Dynamic Media](/help/assets/dm-publish-settings.md).

   ![Configurações de publicação do DM](/help/assets/assets-dm/dm-publish-setup.png)

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>* O [!DNL Experience Manager Forms] lança os pacotes complementares uma semana após a data programada de lançamento do [!DNL Experience Manager] Service Pack.


## Principais recursos em anteriores [!DNL Experience Manager] 6.5 Service Packs {#key-features-previous-service-packs}

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### Recursos incluídos no AEM versão 6.5.10.0 {#features-sites-65100}

* **Aprimorado [!DNL Content Fragment] Modelos e editor**: Agora você pode criar modelos complexos e personalizados para conteúdo estruturado usando [!DNL Content Fragment] modelos. As estruturas de conteúdo são modularizadas em elementos básicos que são modelados como subfragmentos. Os fragmentos de nível superior fazem referência a esses subfragmentos. Mais aprimoramentos de tipo de dados, como regras de validação avançadas, aumentam ainda mais a flexibilidade da modelagem de conteúdo com [!DNL Content Fragments]. O [!DNL Experience Manager] [!DNL Content Fragment] o editor oferece suporte a estruturas de fragmento aninhadas em uma sessão de editor comum, com melhorias como visualização de árvore de estrutura e navegação de navegação estrutural por guias por meio de hierarquias de fragmentos.

* **API GraphQL para[!DNL Content Fragments]**: A nova API GraphQL é o método padrão para fornecer conteúdo estruturado no formato JSON. As consultas GraphQL permitem que os clientes solicitem apenas os itens de conteúdo relevantes para renderizar uma experiência. Essa seleção elimina a entrega excessiva de conteúdo (possibilidade com APIs REST HTTP) que requer análise de conteúdo no lado do cliente. Os esquemas GraphQL são derivados de [!DNL Content Fragment] modelos e as respostas da API são feitas no formato JSON. Em [!DNL Experience Manager] como [!DNL Cloud Service], [As consultas GraphQL persistem](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) e processar solicitações de GET amigáveis ao cache. Ainda não é possível em [!DNL Experience Manager] 6.5.

* **Gerenciamento de hierarquia e pré-visualização futura**: Os usuários agora têm uma interface para acessar as estruturas de conteúdo de seus [!DNL Experience Manager] inicializações, incluindo a capacidade de adicionar e remover páginas em um lançamento. Esse recurso melhora a flexibilidade do [!DNL Experience Manager] inicia para criar versões de conteúdo direcionadas para publicação futura. [Recurso de distorção de tempo](/help/sites-authoring/working-with-page-versions.md#timewarp) permite que os usuários visualizem inicializações como estados de conteúdo futuros.

* [!DNL Experience Manager] exibe diretamente uma lista de todos os modelos de conteúdo em uma pasta, sem que os autores de conteúdo tenham que navegar pela estrutura do arquivo. A funcionalidade agora requer menos cliques e melhora a eficiência da criação.

* Campo de caminho em [!DNL Sites] o editor permite que os autores arraste ativos de [!DNL Content Finder].

* A Platform oferece algumas melhorias de acessibilidade. Consulte [Atualizações da plataforma](/help/release-notes/sp-release-notes.md#platform-65100).

#### Capacidade de restaurar páginas e árvore excluídas (6.5.9.0) {#ability-to-restore-pages-tree}

Agora é possível restaurar as páginas excluídas e a visualização de árvore inteira em um [!DNL Experience Manager Sites] página.

#### Classificar as páginas da Live Copy disponíveis para implantação (6.5.8.0) {#sort-livecopy-pages}

Agora você pode classificar as páginas da Live Copy disponíveis para implantação usando o [!UICONTROL Nome], [!UICONTROL Data da última modificação]e [!UICONTROL Data da última implantação] propriedades. O [!UICONTROL Data da última implantação] para uma página é uma nova propriedade introduzida nesta versão.

#### Disponibilidade de movimentações de página e implantações de MSM como operações assíncronas (6.5.7.0) {#page-moves-msm-asynchronous}

Agora é possível executar movimentações de página e implantações de MSM como operações assíncronas para reduzir seu impacto no desempenho do tempo de execução. Você pode programar as operações para execução imediata ou posterior. O status das tarefas associadas e das etapas do processo é exibido em um console, que é útil para monitorar implantações de MSM em grande escala.

#### Disponibilidade da operação de movimentação de página no modo assíncrono (6.5.6.0) {#page-move-asynchronous}

A operação Mover página agora está disponível no modo assíncrono. Além da execução imediata, você também pode agendar a operação Mover página para execução posterior.

#### Melhorias de acessibilidade (6.5.5.0) {#accessibility-sites}

* Aprimoramento do relatório de erros ao adicionar informações de texto.

* Foco aprimorado na interface do usuário durante a navegação pelo teclado.

* Taxa de contraste aprimorada para vários elementos da interface do usuário.

* Consistência aprimorada de atributos alt para imagens de página.

* Consistência aprimorada de rótulos ARIA (Accessible Rich Internet Applications).

* Melhorias nos recursos de Acesso não visual a desktop (NVDA).

* Aprimoramento do suporte ao leitor de tela.

#### Outras melhorias importantes (6.5.5.0) {#other-enhancements-sites}

* O acesso anônimo ao CRXDE Lite não tem permissão para melhorar a segurança. Em vez disso, os usuários são direcionados para a tela de logon. Consulte [Desenvolvimento com o CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Ao copiar ou colar uma árvore de página, agora há a opção de colar a página raiz ou colar a página raiz com as subpáginas da árvore.

* [!DNL Adobe Experience Manager Experience Fragments] exportados para [!DNL Adobe Target] os espaços de trabalho agora aparecem como tipos de oferta exclusivos e fontes de oferta em [!DNL Target].

* Gerenciador de vários sites - o acionador Publicar agora exclui um componente da página publicada se um componente for excluído da página de origem.

* Gerenciador de vários sites - quando o nome de um componente local em um [!UICONTROL Live Copy] é idêntico ao nome de um componente no blueprint, e o componente é implementado a partir do blueprint, em seguida, o termo `_msm_moved` agora é adicionado ao nome do componente local.

#### Aprimoramentos do sistema de estilos (6.5.4.0) {#style-system-enhancements}

Agora é possível selecionar estilos na caixa de diálogo do componente usando o Sistema de estilos aprimorado.

#### Melhorias de desempenho em várias áreas (6.5.4.0) {#performance-improvements}

* Redução do tempo para carregar e inicializar o ContextHub em um site (`contexthub.kernel.js`). Isso resulta em carregamentos de página mais rápidos durante uma visita ao site.

* Redução do tempo para atualizar uma página após arrastar [!DNL Experience Fragments] para [!DNL Sites] Editor de páginas.

* Tempo de carregamento reduzido para entradas em um [!DNL Sites] página com mais de 200 live copies em **[!UICONTROL Visão geral da Live Copy]**.

* Manuseio aprimorado de URLs incompletas ou inválidas. Esses URLs podem atrasar o Editor de modelo.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### Recursos incluídos no AEM versão 6.5.10.0 {#features-assets-65100}

* [!DNL Experience Manager] estende a funcionalidade Ativos conectados ao uso de [!DNL Dynamic Media] imagens nos componentes principais aplicáveis. Consulte [usar o Connected Assets](/help/assets/use-assets-across-connected-assets-instances.md).

* Ao compartilhar ativos e coleções individuais como um link (usando [!UICONTROL Compartilhamento de link] ), os usuários podem escolher se permitem que o destinatário baixe ativos originais, suas representações ou ambos. Consulte [Compartilhar ativos por link](/help/assets/link-sharing.md).

   ![opção para permitir o download somente dos ativos originais, somente das execuções ou de ambos](/help/release-notes/assets/share-assets-as-link.png)

* Quando os usuários baixam ativos compartilhados com eles como um link, eles podem optar por baixar os ativos originais, as representações ou ambos.

* **Limitar subativos gerados**: Os administradores podem limitar o número de subativos que [!DNL Experience Manager] O gera para ativos compostos, como arquivos PDF, PowerPoint, InDesign e Keynote.

   ![limitar a geração de sub-ativos](/help/assets/assets/sub-asset-limit.png)

* Um novo [!DNL Camera Raw] está disponível e é compatível com [!DNL Adobe Camera Raw] v10.4. Consulte [processar imagens usando [!DNL Camera Raw]](/help/assets/camera-raw.md).

#### Versões anteriores {#previous-releases-assets}

* Atualização do nome das localidades e regiões chinesas relacionadas a Hong Kong, Macau e Taiwan, para torná-las consistentes com as opiniões políticas e sociais chinesas (6.5.9.0).

* Uma configuração opcional é introduzida para alterar o uso de maiúsculas e minúsculas nas IDs de email na resposta da API ACP de [!DNL Adobe Experience Manager] (6.5.9.0)

   ![configuração para alterar as IDs de email para minúsculas na resposta ACP de [!DNL Experience Manager]](assets/email-lowcase-config.png)

* O contraste do texto e dos ícones em segundo plano é aprimorado para vários recursos. Essa implementação das diretrizes da Web Content Accessibility Guidelines (WCAG) faz [!DNL Assets] mais acessível para usuários com visão limitada e percepção de cor. Consulte [melhorias de acessibilidade em [!DNL Assets]](sp-release-notes.md#assets-accessibility-6590) (6.5.9.0)
* Ao usar [Funcionalidade Ativos conectados](/help/assets/use-assets-across-connected-assets-instances.md), agora é possível visualizar uma lista de todos os [!DNL Sites] páginas que usam o ativo. Essas referências a um ativo estão disponíveis em um [!UICONTROL Propriedades] página. Isso permite que administradores, profissionais de marketing e bibliotecas tenham uma visão completa do uso dos ativos, permitindo um melhor rastreamento, gerenciamento e consistência da marca (6.5.8.0).

* Ao excluir um ativo referenciado em uma página da Web, [!DNL Experience Manager] exibe um aviso. É possível forçar a exclusão de um ativo referenciado ou verificar e modificar as referências exibidas no [!DNL Properties] página do ativo. Clicar nas referências abre o local e o remoto [!DNL Sites] páginas (6.5.8.0).

* [!DNL Assets] e [!DNL Dynamic Media] oferecem várias melhorias de acessibilidade. Os aprimoramentos estão relacionados à navegação do teclado, ao uso de leitores de tela e a melhorias semelhantes para permitir o uso de tecnologias de assistência (AT). Consulte [[!DNL Assets] melhorias](/help/release-notes/sp-release-notes.md#assets-6570) e [[!DNL Dynamic Media] melhorias](/help/release-notes/sp-release-notes.md#dynamic-media-6570) (6.5.7.0)

* Os usuários podem classificar ativos digitais nas exibições de Cartão e Coluna (6.5.7.0).

#### Aprimoramentos de acessibilidade (6.5.6.0) {#accessibility-assets-6560}

* **Foco aprimorado na interface do usuário durante a navegação pelo teclado**, por exemplo, concentre-se em:

   * `x` ícone em [!UICONTROL Visualização da versão] diálogo de um ativo em [!UICONTROL Linha do tempo].

   * Opções acionáveis da interface do usuário.

   * Campo de email na [!UICONTROL Compartilhar link] e o campo para adicionar grupo de usuários fechado em [!UICONTROL Permissão] guia da pasta [!UICONTROL Propriedades].

* **Funcionalidade aprimorada com teclas do teclado**

   Os usuários podem usar teclas de teclado para arrastar controles no editor de Formulário de esquema de metadados no modo de navegação do leitor de tela.

* **Maior usabilidade para usuários de leitores de tela**, devido ao seguinte:

   * Leitores de tela anunciam a finalidade dos players de vídeo e áudio.

   * Os leitores de tela anunciam a finalidade das opções da interface do usuário para remover as tags selecionadas usando [!UICONTROL Caixa de diálogo de seleção de tags] no ativo [!UICONTROL Propriedades].

   * Os leitores de tela anunciam os cabeçalhos de linha e os itens de linha das tabelas, para que os usuários saibam quais entradas pertencem à mesma linha.

   * Título descritivo e significativo da página de pesquisa.

   * Os leitores de tela anunciam as opções no painel do filtro de pesquisa como opções expansíveis.

#### Outras melhorias em [!DNL Assets] (6.5.6.0) {#other-enhancements-assets-6560}

* Os grupos de usuários associados às pastas (privadas e não privadas) agora são removidos do repositório em [exclusão dessas pastas](/help/assets/private-folder.md#delete-private-folder). No entanto, os grupos de usuários redundantes, órfãos, não utilizados e gerados automaticamente existentes podem ser removidos do repositório usando o JMX.

#### Aprimoramentos de acessibilidade em [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] O agora está mais acessível, em conformidade com as Web Content Accessibility Guidelines (WCAG). A acessibilidade melhorou devido aos seguintes aprimoramentos:

* Muitos elementos, controles, páginas e caixas de diálogo da interface do usuário são amigáveis para leitores de tela.

* Muitos elementos da interface do usuário, controles e campos de formulário de entrada podem ser acessados pelo teclado.

* A cor e o contraste de alguns elementos da interface do usuário são atualizados para que os usuários com visão limitada ou usuários sem percepção de cor possam distinguir esses elementos da interface do usuário. Por exemplo, a cor dos ícones de classificação de estrelas (como em [!UICONTROL Classificação] seção de [!UICONTROL Avançado] guia no ativo [!UICONTROL Propriedades] ou na exibição de cartão) é alterada para obter o contraste apropriado.

   ![Ícones de classificação com melhor contraste](assets/star-rating-icons.png)

#### Tratamento de exceções aprimorado (6.5.5.0) {#exception-handling}

[!DNL Assets] o fluxo da interface do usuário tem melhor tratamento de exceções. Se um ativo não tiver um tipo para sua dimensão, a exceção observada será registrada nos arquivos de log.

#### Configurar [!DNL Experience Manager Assets] com [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

O canal de autorização entre [!DNL Experience Manager Assets] e [!DNL Brand Portal] é alterada. Anteriormente, [!DNL Brand Portal] O foi configurado na interface clássica por meio do Gateway OAuth herdado, que usa a troca de token JWT para obter um token de acesso IMS para autorização. [!DNL Experience Manager Assets] agora está configurado com [!DNL Brand Portal] through [!DNL Adobe I/O], que obtém um token IMS para autorização de seu [!DNL Brand Portal] inquilino.

As etapas para configurar [!DNL Experience Manager Assets] com [!DNL Brand Portal] são diferentes, dependendo de [!DNL Experience Manager] e se você está configurando pela primeira vez ou atualizando as configurações existentes. Consulte [Configurar o Experience Manager Assets com o Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) para obter detalhes.

#### Aprimoramentos de acessibilidade (6.5.4.0) {#accessibility-enhancements-6540}

[!DNL Experience Manager Assets] O inclui os seguintes aprimoramentos de acessibilidade:

* Teclas de seta no teclado podem ser usadas para mover e deslocar áreas dentro de imagens com zoom. Para obter mais informações, consulte [visualizar ativos usando apenas teclas do teclado](../assets/manage-assets.md#previewing-assets).

* As caixas de seleção de estado misto (nas quais, a menos que você selecione todos os predicados aninhados, as caixas de seleção de primeiro nível não são selecionadas e passam por elas) no painel Filtros são legíveis por leitores de tela.

* As restrições de formato de data e hora são fornecidas nos rótulos de campo dos campos de data, para permitir que os usuários insiram a data no formato correto usando o teclado.
Por exemplo, `On Time (MM-DD-YYYY HH:mm)`. Aqui MM é mês em formato de dois dígitos, AAAA é ano, DD é dia em formato de dois dígitos, HH é hora em formato militar de 24 horas e mm é minuto.

* Os leitores de tela anunciam a opção de remover as tags selecionadas (`X` ) e o número das tags selecionadas.

#### Coluna classificável para a Data de criação dos ativos na exibição de lista (6.5.3.0) {#sortable-date-created-column}

Uma nova coluna classificável para a data de criação dos ativos é adicionada na exibição de lista do DAM e nos resultados da pesquisa de ativos na exibição de lista.

![Coluna classificável para data de criação](assets/asset-created-date.png)

#### Pesquisa visual para [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets]Os usuários do podem pesquisar imagens visualmente semelhantes. O Experience Manager exibe as imagens com tags inteligentes do repositório DAM que são semelhantes a uma imagem selecionada pelo usuário. Consulte [Pesquisa visual](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

* Muitas melhorias de acessibilidade são realizadas em [!DNL Dynamic Media] cliente para que um leitor de tela possa apresentar uma descrição mais apropriada e útil da ação ou interface do usuário. Consulte [[!DNL Dynamic Media] atualizações](/help/release-notes/sp-release-notes.md#dynamic-media-65100) (6.5.10.0)

* [[!DNL Dynamic Media] é mais acessível](sp-release-notes.md#assets-accessibility-6590) em termos de:

   * Facilidade de uso com teclas do teclado.
   * O contraste (com fundo) do texto, do texto de espaço reservado e dos controles em vários editores.
   * Acessibilidade e narração por leitores de tela.

* Fornece imagens de melhor qualidade com eficiência em dispositivos com exibições de alta resolução e largura de banda de rede restrita, com DPR (Device Pixel Ratio) de imagem inteligente e otimização da largura de banda da rede. Consulte [Perguntas frequentes sobre imagens inteligentes](/help/assets/imaging-faq.md) (6.5.9.0)

* [!DNL Dynamic Media] delivery (`fmt` O modificador de URL agora é compatível com o formato de imagem de próxima geração AVIF (formato AV1 Image ). Para obter mais detalhes e linha do tempo, consulte [fmt da API de disponibilização e renderização de imagens](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html) (6.5.9.0)

#### Suporte para ativos 3D no [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

Suporte para imagens 3D em [!DNL Dynamic Media] permite que os clientes publiquem e adicionem conteúdo 3D em páginas e aplicativos da Web. O suporte inclui:

* Publique formatos comuns de ativos 3D e gere um URL de ativo que possa ser usado em páginas da Web e outros aplicativos.

* Um Web Viewer 3D, fornecido por [!DNL Adobe Dimension], para visualizar interativamente os ativos 3D publicados.

* Publicar e exibir ativos 3D comuns em [!DNL Experience Manager Sites] páginas que usam o [!DNL Sites] componente WCM.

#### Invalidar o conteúdo em cache do CDN (6.5.6.0) {#invalidate-cdn-cached-content}

Agora você pode usar o [!DNL Dynamic Media] interface do usuário para invalidar o conteúdo em cache do Content Delivery Network (CDN). Como resultado, os ativos atualizados estão disponíveis instantaneamente em vez de esperar que o cache expire. Você pode invalidar o CDN ao:

* Criando um modelo de invalidação de CDN: Seleção de ativos e URLs com base em modelo associados ao formulário

* Seleção de ativos e predefinições associadas por meio do seletor de ativos

* Adicionar URLs completos do ativo

#### Publicação seletiva de ativos em [!DNL Experience Manager] e [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

Agora é possível optar por publicar ou cancelar a publicação seletiva de ativos em [!DNL Experience Manager] ou [!DNL Dynamic Media] usar [!UICONTROL Publicação rápida] ou [!UICONTROL Gerenciar publicação] assistente. Também é possível definir a variável `Publish` ou `Unpublish` no nível da pasta.

#### Imagem inteligente para Dynamic Media {#smart-imaging}

A geração de imagens inteligentes usa as características de visualização exclusivas de cada usuário para fornecer automaticamente as imagens certas, otimizadas para sua experiência, resultando em melhor desempenho e envolvimento. A geração de imagens inteligentes funciona com as predefinições de imagens existentes e usa inteligência nos últimos milissegundos do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte [Imagens inteligentes](../assets/imaging-faq.md).

#### Recorte inteligente em perfis de vídeo para Dynamic Media (6.5.3.0) {#smart-crop-video}

Recorte inteligente para vídeo - um recurso opcional disponível em Perfis de vídeo - usa o Adobe Sensei para detectar e recortar automaticamente o ponto focal em qualquer vídeo adaptável ou vídeo progressivo, independentemente do tamanho. Consulte [sobre o uso do recorte inteligente em perfis de vídeo](../assets/video-profiles.md).

### Formulários do Experience Manager {#aem-forms-previous-service-packs}

#### Recursos incluídos no AEM versão 6.5.10.0 {#features-forms-65100}

>[!NOTE]
>
>O pacote complementar de [!DNL Experience Manager Forms] é disponibilizado uma semana após a [!DNL Experience Manager] Versão do Service Pack.

* Agora você pode usar o serviço Automated forms conversion para [converter PDF forms em francês, alemão, espanhol, italiano e português](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html#language-specific-meta-model) para formulários adaptáveis.

* **Mensagens de erro no navegador Propriedades**: Adicionadas mensagens de erro para cada propriedade no navegador Adaptive Forms Properties. Essas mensagens ajudam a entender os valores permitidos para um campo.

* **Suporte para usar a opção literal para definir valor para uma variável do tipo JSON**: Você pode usar a opção literal para definir um valor para uma variável do tipo JSON na etapa Definir variável de um fluxo de trabalho AEM. A opção literal permite especificar um JSON no formato de uma string.

* [Atualizações da plataforma](../forms/using/aem-forms-jee-supported-platforms.md): [!DNL Adobe Experience Manager Forms] O JEE adicionou suporte às seguintes plataformas:
   * [!DNL Adobe Acrobat 2020]
   * [!DNL Ubuntu 20.04]
   * [!DNL Open Office 4.1.10]
   * [!DNL Microsoft Office 2019]
   * [!DNL Microsoft Windows Server 2019]
   * [!DNL RHEL8]

* Suporte adicionado para `GuideBridge#getGuidePath` API em [!DNL AEM Forms].

#### Suporte para [!DNL Azul Zulu OpenJDK] (6.5.9.0) {#support-azul-zulu}

Agora você pode desenvolver e operar aplicativos com [!DNL Azul Zulu] construções de [!DNL OpenJDK] para [!DNL Experience Manager Forms] em implantações OSGi. Para obter mais informações, consulte [Notas de versão do Experience Manager 6.5 Service Pack 9](sp-release-notes.md) e [Requisitos técnicos](../sites-deploying/technical-requirements.md).

#### Capacidade de enviar um email de notificação para um grupo usando [!UICONTROL Atribuir tarefa] (6.5.9.0) {#group-notification-email}

Agora é possível enviar um email de notificação para um endereço de email de grupo usando a etapa do fluxo de trabalho Atribuir tarefa .

#### Capacidade de recuperar um rascunho de Comunicação interativa após modificar a fonte Comunicação interativa (6.5.9.0) {#retrieve-draft-after-source-modifications}

Agora é possível recuperar uma comunicação interativa salva como rascunho depois de alterar a fonte Comunicação interativa.

#### Definir nome de domínio personalizado para carregar, renderizar e validar o serviço reCAPTCHA (6.5.9.0) {#set-custom-domain-name-recaptcha}

O serviço reCAPTCHA usa `https://www.recaptcha.net/` como o domínio padrão. Agora você pode modificar as configurações para definir `https://www.google.com/` ou qualquer nome de domínio personalizado para carregar, renderizar e validar o serviço reCAPTCHA.

#### Melhorias de dados de entrada para [!UICONTROL Chamar Serviço de Modelo de Dados de Formulário] etapa do fluxo de trabalho (6.5.9.0) {#input-data-enhancements-fdm}

Ao selecionar um modelo de dados de formulário e um serviço em [!UICONTROL Chamar Serviço de Modelo de Dados de Formulário] etapa do fluxo de trabalho, especifique argumentos de serviço para dados de entrada.

Se você selecionar [!UICONTROL Em relação à carga] para anexar um arquivo como um argumento de serviço, agora é possível especificar o caminho da pasta que contém o arquivo em vez do nome do arquivo real. Definir o nome da pasta, em vez do nome do anexo do arquivo, permite reutilizar modelos de fluxo de trabalho. Você não limita o modelo de fluxo de trabalho a um único nome de anexo de arquivo.

#### Capacidade de usar várias páginas principais em um modelo de Documento de registro (6.5.9.0) {#use-multiple-master-pages-dor-template}

Agora você pode usar várias páginas principais em um modelo de Documento de registro. Como resultado, agora você pode ter cabeçalho, rodapé, fontes, informações de logotipo diferentes na página de título e outras páginas do modelo.

#### Quebras de página de suporte no Documento de registro (6.5.9.0) {#support-page-breaks-dor}

Agora é possível adicionar quebras de página a um Documento de registro. Como resultado, se um painel for quebrado em páginas, você poderá adicionar uma quebra de página para mover o painel para uma nova página em um Documento de registro.

#### Mostrar ou ocultar o componente CAPTCHA em um formulário adaptável com base nas regras (6.5.8.0) {#show-hide-captcha}

Agora é possível validar CAPTCHA no envio de formulário adaptável ou na ação do usuário. Você também pode adicionar condições para validar CAPTCHA em uma ação do usuário e mostrar ou ocultar o componente CAPTCHA em um formulário adaptável com base em regras.

#### Adicionar serviços CAPTCHA personalizados (6.5.8.0) {#add-custom-captcha-services}

[!DNL Experience Manager Forms] O fornece suporte pronto para uso para usar o Google reCAPTCHA (é necessária uma licença separada de APIs reCAPTCHA do Google) como um serviço de validação CAPTCHA. Você também pode usar um serviço CAPTCHA personalizado para validar CAPTCHAs.

#### Outras melhorias (6.5.8.0) {#other-enhancements-forms-6580}

* Melhoria na acessibilidade do [!DNL Experience Manager Forms] Componente Seletor de data.

* Adição de suporte para gerar uma Comunicação interativa no formato PCL usando a API PrintChannel.

* Ao executar uma conversão PDFG, agora é possível ativar ou desativar o [!DNL Experience Manager Forms] alterações no registro para geração de marcadores personalizados.

#### Melhorias de desempenho (6.5.7.0) {#performance-improvements-forms}

[!DNL Experience Manager] 6.5 O Service Pack 7 do Forms melhora o desempenho para:

* Validação dos valores de campo no servidor ao enviar um formulário adaptável.

* Conversão de um formulário PDF para um formulário adaptável usando o [!DNL Automated Forms Conversion service].

#### Suporte para grupos de disponibilidade Always On do Microsoft SQL Server 2016 para Alta Disponibilidade (6.5.7.0) {#always-on-availability-groups}

[!DNL Experience Manager Forms] agora suporta [!DNL Microsoft] Grupos de disponibilidade Always On do SQL Server 2016 para Alta Disponibilidade para implantações OSGi.

#### Modelo de dados de formulário Configuração do cliente HTTP para otimizar o desempenho (6.5.7.0) {#fdm-http-client-config}

[!DNL Experience Manager Forms] O modelo de dados de formulário ao integrar com serviços da Web RESTful como fonte de dados agora inclui configurações de cliente HTTP para otimização de desempenho. Consulte [Configurar fontes de dados](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration).

#### Disponibilidade da opção de redefinição para cada componente no modo Layout (6.5.7.0) {#reset-option-layout-mode}

Agora é possível usar a opção de redefinição para cada componente no modo Layout de um formulário adaptável. Ao definir um layout de várias colunas para um painel, você pode usar esse recurso para redefinir componentes individuais dentro do painel. Consulte [Usar o modo de layout para redimensionar componentes](../../help/forms/using/resize-using-layout-mode.md#resize-components).

#### Preencha previamente um formulário adaptável no cliente (6.5.6.0) {#prefill-merge-data-at-client}

Ao preencher previamente um formulário adaptável, a variável [!DNL Experience Manager Forms] O servidor mescla dados com um formulário adaptável e fornece o formulário preenchido para você. Por padrão, a ação de mesclagem de dados ocorre no servidor.
Agora você pode configurar o [!DNL Experience Manager Forms] para [executar a ação de mesclagem de dados no cliente](../../help/forms/using/prepopulate-adaptive-form-fields.md) em vez do servidor. Reduz significativamente o tempo necessário para preencher e renderizar formulários adaptáveis.

#### Integração do modelo de dados de formulário com APIs RESTful em um servidor com implementação SSL bidirecional (6.5.6.0) {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] o modelo de dados de formulário agora pode [integrar com RESTful APIs em um servidor que tenha um SSL bidirecional implementado nele](../../help/forms/using/configure-data-sources.md).

#### Suporte adicionado para [!DNL Adobe Sign] Tags de texto no serviço Automated forms conversion (6.5.6.0) {#sign-integration-acroform-afcs}

Se um formulário macro incluir [!DNL Adobe Sign] Tags de texto, esses campos agora são reconhecidos e representados como [!DNL Adobe Sign] campos no formulário adaptável convertidos usando [!DNL Automated Forms Conversion service]. Um assinante pode preencher esses campos ao assinar o formulário adaptável.

#### Suporte para converter PDF forms coloridos em formulários adaptáveis (6.5.6.0) {#colored-PDF-forms}

Você pode usar [!DNL Automated Forms Conversion service] para converter PDF forms coloridos em formulários adaptáveis.

#### Suporte para protocolos SMB 2 e SMB 3 (6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] agora suporta protocolos SMB 2 e SMB 3.

#### Armazenamento em cache aprimorado para páginas de formulário adaptável traduzidas (6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

Agora você pode especificar [locale como um seletor na URL do formulário adaptável, em vez de um argumento na URL do formulário adaptável](../../help/forms/using/supporting-new-language-localization.md). Ajuda a colocar formulários adaptáveis em cache no [!DNL Experience Manager Dispatcher]. O armazenamento em cache de formulários adaptáveis traduzidos não era possível em versões anteriores. Para obter informações detalhadas sobre como configurar o armazenamento em cache para usar o local como um seletor no URL do formulário adaptável, consulte [Configurar o cache de formulário adaptável no dispatcher](../../help/forms/using/configure-adaptive-forms-cache.md).

#### Salve a saída do serviço de modelo de dados de formulário em uma variável (6.5.6.0) {#save-fdm-service-to-variable}

O modelo de dados de formulário permite salvar a saída de um serviço de modelo de dados de formulário em uma variável. [!DNL Experience Manager Forms] agora mapeia automaticamente o tipo de serviço de modelo de dados de formulário para o tipo de variável.

#### Anexar vários arquivos para o componente Anexo de arquivo (6.5.6.0) {#attach-multiple-files}

Agora você pode [anexar vários arquivos](../../help/forms/using/introduction-forms-authoring.md) para [!UICONTROL Anexo de arquivo] componente de formulários adaptáveis.

#### Personalizar as colunas da Caixa de entrada do Adobe Experience Manager (6.5.5.0) {#customize-aem-inbox-columns}

Você pode personalizar um [!DNL Experience Manager] Caixa de entrada para alterar o título padrão de uma coluna, reorganizar a posição de uma coluna e exibir colunas adicionais com base nos dados de um fluxo de trabalho. Membros de `administrators` ou `workflow-administrators` pode personalizar as colunas. Para obter mais informações, consulte [Controle de administração](../sites-authoring/inbox.md#inbox-admin-control).

![Personalizar colunas da Caixa de entrada do Experience Manager](assets/customize-columns.gif)

#### Salvar comunicações interativas como rascunho (6.5.5.0) {#save-as-draft}

Você pode usar a interface do usuário do agente para salvar um ou mais rascunhos de cada Comunicação interativa e recuperar o rascunho posteriormente para continuar trabalhando nela. Você pode especificar um nome diferente para cada rascunho para identificá-lo. Para obter mais informações, consulte [Salvar comunicações interativas como rascunho](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![Salvar como rascunho](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] suporte ao servidor de aplicativos (6.5.5.0) {#weblogic-support}

A Adobe Experience Manager Forms adicionou suporte para [!DNL Oracle WebLogic 12] para Adobe Experience Manager Forms no JEE. Você pode atualizar de uma versão anterior ou configurar um novo Experience Manager 6.5 Forms no servidor JEE em [!DNL Oracle WebLogic] 12.2.1.4 e posterior. Mais tarde corresponde às alterações de versão secundária, onde x em 12.2.1.x é substituído por um número de versão.

#### Melhorias de acessibilidade (6.5.5.0) {#accessibility-improvements}

O Adobe Experience Manager Forms inclui os seguintes aprimoramentos de acessibilidade:

* Quando um usuário visualiza um formulário adaptável como um formulário HTML, a variável [!UICONTROL Assinatura do Scribble] mantém o foco da guia.

* As mensagens de erro exibidas ao enviar um formulário adaptável agora contêm a variável `aria-describedBy` atributo. O atributo é anexado aos campos mencionados na mensagem de erro. O `aria-describedby` indica as IDs dos elementos que descrevem o objeto. Ajuda a estabelecer uma relação entre widgets ou grupos e texto que os descreveu.

* Se um formulário adaptável tiver alguns campos obrigatórios, o atributo obrigatório será definido como `True` para esses campos no schema de acessibilidade ARIA.

#### Autenticação com certificado X-509 para serviços da Web baseados em SOAP no modelo de dados de formulário (6.5.5.0) {#x509-based-authentication-soap}

O modelo de dados de formulário agora oferece suporte à autenticação baseada em certificado X-509 ao usar serviços da Web SOAP como a fonte de dados. Para obter mais informações, consulte [Configurar serviços Web SOAP](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### Outras melhorias importantes (6.5.5.0) {#other-improvements}

* O Experience Manager 6.5 Forms na Segurança de documentos JEE agora é baseado em [!DNL Apache Struts 2].

* Suporte adicionado para [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### Gerar saída para impressão em workflows do Experience Manager Forms (6.5.4.0) {#generate-printable-output}

A etapa de fluxo de trabalho Gerar saída para impressão permite integrar um arquivo de modelo de origem a um arquivo de dados. Essa integração permite que você imprima ou salve cópias diferentes do arquivo de modelo. A etapa gera uma saída PCL, PostScript, ZPL, IPL, TPCL ou DPL. Para obter mais informações sobre este recurso, consulte [Fluxo de trabalho centrado na Forms no OSGi - Referência em etapas](../forms/using/aem-forms-workflow-step-reference.md).

![Gerar saída para impressão](assets/generate-print-output-step.gif)

#### Suporte a várias colunas para formulários adaptáveis e comunicações interativas no modo Layout (6.5.4.0) {#multi-column-adaptive-forms}

Agora é possível definir o número de colunas para um painel em formulários adaptáveis e comunicações interativas. Alterne para o modo de layout para usar a nova opção de várias colunas. Para obter mais informações, consulte [Usar o modo Layout para redimensionar componentes](../forms/using/resize-using-layout-mode.md).

![Layout de várias colunas](assets/multi-column-layout.gif)

#### Personalizações da Caixa de entrada do Experience Manager (6.5.4.0) {#aem-inbox}

A nova opção Controle de administrador permite que os administradores:

* Personalize o texto e o logotipo do cabeçalho.

* Controlar a exibição de links de navegação disponíveis no cabeçalho.

A opção Controle de administrador está visível somente para os membros do `administrators` ou `workflow-administrators` grupo. Para obter mais informações sobre este recurso, consulte [Sua Caixa de entrada](../sites-authoring/inbox.md).

#### Suporte a rich text em formulários HTML5 (6.5.4.0) {#rich-text-support}

Converta um campo de texto em um formulário XFA em um campo de rich text em um formulário HTML5. Para obter mais informações, consulte [Criação de modelos de formulário para formulários HTML5](../forms/using/designing-form-template.md).

#### Aprimoramentos de acessibilidade (6.5.4.0) {#forms-accessibility-enhancements-6540}

O Experience Manager Forms inclui os seguintes aprimoramentos de acessibilidade:

* Os leitores de tela anunciam as caixas de seleção, os links, o Seletor de data e os campos de Entrada de data corretamente em um formulário adaptável.

* Cada página de um formulário adaptável agora inclui um título e um rótulo principal de marca.

#### Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário do Experience Manager Forms (6.5.3.0) {#share-request-access}

Você pode compartilhar seus itens da Caixa de entrada com outro usuário. Assim que outro usuário tiver acesso aos itens da Caixa de entrada, ele poderá reivindicar e tomar as medidas apropriadas nos itens compartilhados. Da mesma forma, você pode solicitar acesso aos itens da Caixa de entrada de outros usuários. Consulte [Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário](../forms/using/configure-shared-queues-osgi.md).

#### Definir as configurações de ausência do escritório para itens da Caixa de entrada de um usuário do Experience Manager Forms (6.5.3.0) {#configure-out-of-office}

Se você planeja estar fora do escritório, você pode especificar o que acontece com os itens que são atribuídos a você para esse período.
Você tem a opção de especificar uma data e hora de início e uma data e hora de término para que as configurações de ausência do escritório entrem em vigor. Você pode definir uma pessoa padrão para a qual todos os itens são enviados. Consulte [Definir configurações fora do escritório](../forms/using/configure-out-of-office-settings.md).

#### Gerar várias comunicações interativas usando a API em lote para Experience Manager Forms (6.5.3.0) {#generate-multiple-ic}

Você pode usar a API em lote para produzir várias comunicações interativas de um modelo. O modelo é uma comunicação interativa sem dados. A API em lote combina dados com um modelo para produzir uma comunicação interativa. A API é útil na produção em massa de comunicações interativas. Por exemplo, contas telefônicas, demonstrativos de cartão de crédito para vários clientes. Consulte [Gerar várias comunicações interativas usando a API em lote](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

<!-- TBD: Check if the wider team released anything in FY21.
-->

## Versões principais desde [!DNL Adobe Experience Manager] 6.5 SP10{#key-releases-since-last-sp}

Entre 26 de agosto de 2021 e 25 de novembro de 2021, o Adobe lançou o seguinte, além dos Service Packs:

* [!DNL Adobe Experience Manager] as a Cloud Service [2021.9.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-9-0.html) e [2021.10.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

* [[!DNL Experience Manager] aplicativo de desktop 2.1 (2.1.3.4)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Experience Manager Screens: Feature Pack 202109](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202109.html)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Documentação 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR)
>* [Notas de versão gerais de disponibilidade para [!DNL Experience Manager] 6,5](release-notes.md)
>* [Notas de versão do Service Pack para [!DNL Experience Manager] 6,5](sp-release-notes.md)

