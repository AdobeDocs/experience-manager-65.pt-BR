---
title: Novidades do  [!DNL Experience Manager] 6.5 Service Pack 9
description: Novidades do  [!DNL Experience Manager] 6.5 Service Pack 9
contentOwner: AK
mini-toc-levels: 1
exl-id: 32470e6e-8a66-4670-82da-2259f6e001c3
source-git-commit: 29e045ef3080866a94e0925bc0c176a91092c729
workflow-type: tm+mt
source-wordcount: '3726'
ht-degree: 1%

---

# Novidades do [!DNL Adobe Experience Manager] 6.5 Service Pack 9 {#aem-whats-new-service-pack}

![Novidades](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 Os Service Packs oferecem novos recursos, melhorias solicitadas pelo cliente e melhorias de desempenho, estabilidade e segurança em intervalos trimestrais. A disponibilidade trimestral facilita o acesso e a adoção de novos recursos e inovações.

Este artigo destaca os recursos incluídos no Service Pack mais recente, [principais recursos incluídos nos 6.5 Service Packs anteriores](#key-features-previous-service-packs), e as [versões de chave desde a última versão do Service Pack](#key-releases-since-last-sp).

>[!NOTE]
>
>A partir do AEM Service Pack 9, [!DNL Experience Manager] os clientes podem desenvolver e operar seus aplicativos [!DNL Experience Manager] com distribuições dos [!DNL Azul Zulu] builds of OpenJDK, compatíveis com padrões do Java SE.
>O suporte para [!DNL Azul Zulu] JDKs também é fornecido pelo Adobe aos clientes [!DNL Experience Manager].
>Você pode baixar as versões relevantes dos JDKs [!DNL Azul Zulu] de [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
>Os direitos de uso da tecnologia Oracle Java, conforme distribuídos pelo Adobe, expirarão no final de dezembro de 2022. [!DNL Experience Manager] os clientes do são incentivados a planejar e implementar o uso dos  [!DNL Azul Zulu] JDKs mais recentes até essa data. Para obter mais informações sobre o uso da tecnologia [!DNL Oracle Java] e da tecnologia [!DNL Azul Zulu], consulte as [Perguntas frequentes](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf?lang=en) associadas.

## [!DNL Adobe Experience Manager Sites] {#aem-sites}

### Capacidade de restaurar páginas e árvore excluídas {#ability-to-restore-pages-tree}

Agora é possível restaurar as páginas excluídas e a visualização de árvore inteira em uma página [!DNL Experience Manager Sites].

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* Atualização do nome de localidades e regiões chinesas relacionadas a Hong Kong, Macau e Taiwan, para torná-las consistentes com as visões sociais e políticas chinesas.

* Uma configuração opcional é introduzida para minorar as IDs de email na resposta da api ACP de [!DNL Adobe Experience Manager].

   ![configuração para minúsculas as IDs de email na resposta ACP do AEM](assets/email-lowcase-config.png)

* O contraste (com fundo) do texto e dos ícones em vários lugares é aprimorado de acordo com a WCAG, para torná-lo acessível para usuários com visão limitada e percepção de cor. Para obter mais informações, consulte [Aprimoramentos de acessibilidade em Ativos](sp-release-notes.md#assets-accessibility-6590).

### Dynamic Media {#assets-dynamic-media}

* [A mídia dinâmica é mais ](sp-release-notes.md#assets-accessibility-6590) acessível em termos de:

   * facilidade de uso com teclas do teclado.
   * contraste (com plano de fundo) do texto, texto de espaço reservado e controles em vários editores.
   * acessibilidade e narração por leitores de tela.

* O DPR de Smart Imaging (Device Pixel Ratio) e a otimização da largura de banda da rede permitem que você forneça imagens de melhor qualidade com eficiência; em dispositivos com telas de alta resolução e largura de banda de rede restrita. Para obter mais informações, consulte [Perguntas frequentes sobre imagem inteligente](/help/assets/imaging-faq.md).

   >[!NOTE]
   >
   >A linha do tempo da versão para os aprimoramentos de Smart Imaging acima é:
   >
   >* América do Norte 24 de maio de 2021 em NA,
      >
      >
   * Europa, Oriente Médio e África 25 de junho de 2021,
      >
      >
   * Ásia-Pacífico em 19 de julho de 2021.


* Introdução do suporte para o formato de imagem da próxima geração AVIF na entrega do Dynamic Media (modificador de URL fmt). Para obter mais informações, consulte [image service and rendering api fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html).

   >[!NOTE]
   >
   >A linha do tempo da versão do suporte a AVIF é:
   >
   >* América do Norte, 10 de maio de 2021,
      >
      >
   * Europa, Oriente Médio e África 24 de maio de 2021,
      >
      >
   * Ásia-Pacífico, 24 de junho de 2021.


## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>O pacote complementar de [!DNL Experience Manager Forms] é disponibilizado uma semana após a versão agendada do [!DNL Experience Manager] Service Pack.

### Suporte para [!DNL Azul Zulu OpenJDK] {#support-azul-zulu}

Agora você pode desenvolver e operar aplicativos com [!DNL Azul Zulu] criações de [!DNL OpenJDK] para [!DNL Experience Manager Forms] em implantações OSGi. Para obter mais informações, consulte [Notas de versão do Experience Manager 6.5 Service Pack 9](sp-release-notes.md) e [Requisitos técnicos](../sites-deploying/technical-requirements.md).

### Capacidade de enviar um email de notificação para um grupo usando [!UICONTROL Atribuir tarefa] {#group-notification-email}

Agora é possível enviar um email de notificação para um endereço de email de grupo usando a etapa do fluxo de trabalho Atribuir tarefa .

### Capacidade de recuperar um rascunho de Comunicação Interativa após modificar a fonte Comunicação Interativa {#retrieve-draft-after-source-modifications}

Agora é possível recuperar uma comunicação interativa salva como rascunho depois de fazer alterações na origem da Comunicação Interativa.

### Definir nome de domínio personalizado para carregar, renderizar e validar o serviço reCAPTCHA {#set-custom-domain-name-recaptcha}

O serviço reCAPTCHA usa `https://www.recaptcha.net/` como o domínio padrão. Agora você pode modificar as configurações para definir `https://www.google.com/` ou qualquer nome de domínio personalizado para carregar, renderizar e validar o serviço reCAPTCHA.

### Aprimoramentos de dados de entrada para [!UICONTROL Invoke Form Data Model Service] etapa do fluxo de trabalho {#input-data-enhancements-fdm}

Ao selecionar um modelo de dados de formulário e um serviço na etapa de fluxo de trabalho [!UICONTROL Invoke Form Data Model Service], você especifica os argumentos de serviço para dados de entrada.

Se você selecionar a opção [!UICONTROL Relative to Payload] para anexar um arquivo como um argumento de serviço, agora será possível especificar o caminho da pasta que contém o arquivo em vez do nome real do arquivo. Definir o nome da pasta, em vez do nome do anexo do arquivo, permite reutilizar modelos de fluxo de trabalho. Você não limita o modelo de fluxo de trabalho a um único nome de anexo de arquivo.

### Capacidade de usar várias páginas principais em um modelo de Documento de registro {#use-multiple-master-pages-dor-template}

Agora você pode usar várias páginas principais em um modelo de Documento de registro. Como resultado, agora você pode ter cabeçalho, rodapé, fontes, informações de logotipo diferentes na página de título e outras páginas do modelo.

### Suporte a quebras de página no Documento de registro {#support-page-breaks-dor}

Agora é possível adicionar quebras de página a um Documento de registro. Como resultado, se um painel for quebrado em páginas, você poderá adicionar uma quebra de página para mover o painel para uma nova página em um Documento de registro.

## Principais recursos dos [!DNL Experience Manager] 6.5 Service Packs {#key-features-previous-service-packs} anteriores

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### Classifique as páginas da Live Copy disponíveis para implantação (6.5.8.0) {#sort-livecopy-pages}

Agora é possível classificar as páginas da Live Copy disponíveis para implantação usando as propriedades [!UICONTROL Name], [!UICONTROL Last modified date] e [!UICONTROL Last rollout date]. A [!UICONTROL Data da última implementação] de uma página é uma nova propriedade introduzida nesta versão.

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

* O acesso anônimo ao CRXDE Lite não tem permissão para melhorar a segurança. Em vez disso, os usuários são direcionados para a tela de logon. Consulte [Desenvolvimento com CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Ao copiar ou colar uma árvore de página, agora há a opção de colar a página raiz ou colar a página raiz com as subpáginas da árvore.

* [!DNL Adobe Experience Manager Experience Fragments] exportados para  [!DNL Adobe Target] espaços de trabalho agora aparecem como tipos de oferta exclusivos e fontes de oferta no  [!DNL Target].

* Gerenciador de vários sites - o acionador Publicar agora exclui um componente da página publicada se um componente for excluído da página de origem.

* Gerenciador de vários sites - Quando o nome de um componente local em uma [!UICONTROL Live Copy] é idêntico ao nome de um componente no blueprint e o componente é implementado no blueprint, o termo `_msm_moved` agora é adicionado ao nome do componente local.

#### Aprimoramentos do sistema de estilos (6.5.4.0) {#style-system-enhancements}

Agora é possível selecionar estilos na caixa de diálogo do componente usando o Sistema de estilos aprimorado.

#### Melhorias de desempenho em várias áreas (6.5.4.0) {#performance-improvements}

* Redução do tempo para carregar e inicializar o ContextHub em um site (`contexthub.kernel.js`). Isso resulta em carregamentos de página mais rápidos durante uma visita ao site.

* Redução do tempo para atualizar uma página depois de arrastar [!DNL Experience Fragments] para [!DNL Sites] Editor de página.

* Tempo de carregamento reduzido para entradas em uma página [!DNL Sites] com mais de 200 cópias ativas em **[!UICONTROL Visão geral da Live Copy]**.

* Manuseio aprimorado de URLs incompletas ou inválidas. Esses URLs podem atrasar o Editor de modelo.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

* Ao usar [a funcionalidade Ativos conectados](/help/assets/use-assets-across-connected-assets-instances.md), agora é possível visualizar uma lista de todas as páginas [!DNL Sites] que usam o ativo. Essas referências a um ativo estão disponíveis na página [!UICONTROL Propriedades] de um ativo. Isso permite que administradores, profissionais de marketing e bibliotecas tenham uma visão completa do uso dos ativos, permitindo um melhor rastreamento, gerenciamento e consistência da marca (6.5.8.0).

* Ao excluir um ativo referenciado em uma página da Web, [!DNL Experience Manager] exibe um aviso. É possível forçar a exclusão de um ativo referenciado ou verificar e modificar as referências exibidas na página [!DNL Properties] do ativo. Clicar nas referências abre as páginas locais e remotas [!DNL Sites] (6.5.8.0).

* [!DNL Assets] e  [!DNL Dynamic Media] oferecem várias melhorias de acessibilidade. Os aprimoramentos estão relacionados à navegação do teclado, ao uso de leitores de tela e a melhorias semelhantes para permitir o uso de tecnologias de assistência (AT). Consulte [[!DNL Assets] aprimoramentos](/help/release-notes/sp-release-notes.md#assets-6570) e [[!DNL Dynamic Media] aprimoramentos](/help/release-notes/sp-release-notes.md#dynamic-media-6570) (6.5.7.0)

* Os usuários podem classificar ativos digitais nas exibições de Cartão e Coluna (6.5.7.0).

#### Aprimoramentos de acessibilidade (6.5.6.0) {#accessibility-assets-6560}

* **Foco aprimorado na interface do usuário durante a navegação** do teclado, por exemplo, foco em:

   * `x` ícone na caixa de diálogo  [!UICONTROL Visualização de ] versão de um ativo na  [!UICONTROL Linha do tempo].

   * Opções acionáveis da interface do usuário.

   * Campo de email na caixa de diálogo [!UICONTROL Compartilhar link] e campo para adicionar grupo de usuários fechado na guia [!UICONTROL Permissão] da pasta [!UICONTROL Propriedades].

* **Funcionalidade aprimorada com teclas do teclado**

   Os usuários podem usar teclas de teclado para arrastar controles no editor de Formulário de esquema de metadados no modo de navegação do leitor de tela.

* **Maior usabilidade para usuários** de leitores de tela devido ao seguinte:

   * Leitores de tela anunciam a finalidade dos players de vídeo e áudio.

   * Os leitores de tela anunciam a finalidade das opções da interface do usuário para remover as tags selecionadas usando a caixa de diálogo [!UICONTROL Tags selection] no ativo [!UICONTROL Properties].

   * Os leitores de tela anunciam os cabeçalhos de linha e os itens de linha das tabelas, para que os usuários saibam quais entradas pertencem à mesma linha.

   * Título descritivo e significativo da página de pesquisa.

   * Os leitores de tela anunciam as opções no painel do filtro de pesquisa como opções expansíveis.

#### Outras melhorias em [!DNL Assets] (6.5.6.0) {#other-enhancements-assets-6560}

* Os grupos de usuários associados a pastas (privadas e não privadas) agora são removidos do repositório em [exclusão dessas pastas](/help/assets/private-folder.md#delete-private-folder). No entanto, os grupos de usuários redundantes, órfãos, não utilizados e gerados automaticamente existentes podem ser removidos do repositório usando o JMX.

#### Aprimoramentos de acessibilidade em [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] O agora está mais acessível, em conformidade com as Web Content Accessibility Guidelines (WCAG). A acessibilidade melhorou devido aos seguintes aprimoramentos:

* Muitos elementos, controles, páginas e caixas de diálogo da interface do usuário são amigáveis para leitores de tela.

* Muitos elementos da interface do usuário, controles e campos de formulário de entrada podem ser acessados pelo teclado.

* A cor e o contraste de alguns elementos da interface do usuário são atualizados para que os usuários com visão limitada ou usuários sem percepção de cor possam distinguir esses elementos da interface do usuário. Por exemplo, a cor dos ícones de classificação de estrelas (como na seção [!UICONTROL Classificação] da guia [!UICONTROL Avançado] no ativo [!UICONTROL Propriedades] ou na exibição de cartão) é alterada para obter o contraste apropriado.

   ![Ícones de classificação com melhor contraste](assets/star-rating-icons.png)

#### Tratamento de exceções aprimorado (6.5.5.0) {#exception-handling}

[!DNL Assets] o fluxo da interface do usuário tem melhor tratamento de exceções. Se um ativo não tiver um tipo para sua dimensão, a exceção observada será registrada nos arquivos de log.

#### Suporte para ativos 3D em [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

O suporte para imagens 3D em [!DNL Dynamic Media] permite que os clientes publiquem e adicionem conteúdo 3D em páginas e aplicativos da Web. O suporte inclui:

* Publique formatos comuns de ativos 3D e gere um URL de ativo que possa ser usado em páginas da Web e outros aplicativos.

* Um Visualizador da Web 3D, desenvolvido por [!DNL Adobe Dimension], para visualizar interativamente os ativos 3D publicados.

* Publique e visualize ativos 3D comuns em [!DNL Experience Manager Sites] páginas usando o componente [!DNL Sites] WCM.

#### Configure [!DNL Experience Manager Assets] com [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

O canal de autorização entre [!DNL Experience Manager Assets] e [!DNL Brand Portal] é alterado. Anteriormente, [!DNL Brand Portal] era configurado na interface clássica por meio do Gateway OAuth herdado, que usa a troca de token JWT para obter um token de Acesso IMS para autorização. [!DNL Experience Manager Assets] O agora é configurado com o  [!DNL Brand Portal] por meio do  [!DNL Adobe I/O], que obtém um token IMS para autorização do  [!DNL Brand Portal] locatário.

As etapas para configurar [!DNL Experience Manager Assets] com [!DNL Brand Portal] são diferentes dependendo da sua versão [!DNL Experience Manager] e se você está configurando pela primeira vez ou atualizando as configurações existentes. Consulte [Configurar ativos do Experience Manager com Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) para obter detalhes.

#### Aprimoramentos de acessibilidade (6.5.4.0) {#accessibility-enhancements-6540}

[!DNL Experience Manager Assets] O inclui os seguintes aprimoramentos de acessibilidade:

* Teclas de seta no teclado podem ser usadas para mover e deslocar áreas dentro de imagens com zoom. Para obter mais informações, consulte [visualizar ativos usando apenas teclas do teclado](../assets/manage-assets.md#previewing-assets).

* As caixas de seleção de estado misto (nas quais, a menos que você selecione todos os predicados aninhados, as caixas de seleção de primeiro nível não são selecionadas e passam por elas) no painel Filtros são legíveis por leitores de tela.

* As restrições de formato de data e hora são fornecidas nos rótulos de campo dos campos de data, para permitir que os usuários insiram a data no formato correto usando o teclado.
Por exemplo, `On Time (MM-DD-YYYY HH:mm)`. Aqui MM é mês em formato de dois dígitos, AAAA é ano, DD é dia em formato de dois dígitos, HH é hora em formato militar de 24 horas e mm é minuto.

* Os leitores de tela anunciam a opção de remover as tags selecionadas (símbolo`X`) e o número das tags selecionadas.

#### Coluna classificável para a Data de criação dos ativos na exibição de lista (6.5.3.0) {#sortable-date-created-column}

Uma nova coluna classificável para a data de criação dos ativos é adicionada na exibição de lista do DAM e nos resultados da pesquisa de ativos na exibição de lista.

![Coluna classificável para data de criação](assets/asset-created-date.png)

#### Pesquisa visual por [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets]Os usuários do podem pesquisar imagens visualmente semelhantes. O Experience Manager exibe as imagens com tags inteligentes do repositório DAM que são semelhantes a uma imagem selecionada pelo usuário. Consulte [Pesquisa visual](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Invalidar o conteúdo em cache do CDN (6.5.6.0) {#invalidate-cdn-cached-content}

Agora você pode usar a interface do usuário [!DNL Dynamic Media] para invalidar o conteúdo em cache da Rede de entrega de conteúdo (CDN). Como resultado, os ativos atualizados estão disponíveis instantaneamente em vez de esperar que o cache expire. Você pode invalidar o CDN ao:

* Criando um modelo de invalidação de CDN: Seleção de ativos e URLs com base em modelo associados ao formulário

* Seleção de ativos e predefinições associadas por meio do seletor de ativos

* Adicionar URLs completos do ativo

#### Publicação seletiva de ativos em [!DNL Experience Manager] e [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

Agora é possível optar por publicar ou cancelar a publicação seletiva de ativos em [!DNL Experience Manager] ou [!DNL Dynamic Media] usando o assistente [!UICONTROL Publicação rápida] ou [!UICONTROL Gerenciar publicação]. Você também pode definir o modo `Publish` ou `Unpublish` no nível da pasta.

#### Imagem inteligente para Dynamic Media {#smart-imaging}

A geração de imagens inteligentes usa as características de visualização exclusivas de cada usuário para fornecer automaticamente as imagens certas, otimizadas para sua experiência, resultando em melhor desempenho e envolvimento. A geração de imagens inteligentes funciona com as predefinições de imagens existentes e usa inteligência nos últimos milissegundos do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte [Imagens inteligentes](../assets/imaging-faq.md).

#### Recorte inteligente em perfis de vídeo para Dynamic Media (6.5.3.0) {#smart-crop-video}

Recorte inteligente para vídeo - um recurso opcional disponível em Perfis de vídeo - é uma ferramenta que usa o poder da inteligência artificial no Adobe Sensei para detectar e recortar automaticamente o ponto focal em qualquer vídeo adaptável ou vídeo progressivo que você tenha carregado, independentemente do tamanho. Consulte [Sobre como usar o recorte inteligente em perfis de vídeo](../assets/video-profiles.md).

### Formulários do Experience Manager {#aem-forms-previous-service-packs}

#### Mostrar ou ocultar o componente CAPTCHA em um formulário adaptável com base em regras (6.5.8.0) {#show-hide-captcha}

Agora é possível validar CAPTCHA no envio de formulário adaptável ou na ação do usuário. Você também pode adicionar condições para validar CAPTCHA em uma ação do usuário e mostrar ou ocultar o componente CAPTCHA em um formulário adaptável com base em regras.

#### Adicionar serviços CAPTCHA personalizados (6.5.8.0) {#add-custom-captcha-services}

[!DNL Experience Manager Forms] O fornece suporte pronto para uso para usar o Google reCAPTCHA (é necessária uma licença separada de APIs do Google reCAPTCHA) como um serviço de validação CAPTCHA. Você também pode usar um serviço CAPTCHA personalizado para validar CAPTCHAs.

#### Outras melhorias (6.5.8.0) {#other-enhancements-forms-6580}

* Melhoria na acessibilidade do componente [!DNL Experience Manager Forms] do Seletor de datas.

* Adição de suporte para gerar uma Comunicação interativa no formato PCL usando a API PrintChannel.

* Ao executar uma conversão PDFG, agora é possível ativar ou desativar as alterações de registro [!DNL Experience Manager Forms] para geração de marcadores personalizados.

#### Melhorias de desempenho (6.5.7.0) {#performance-improvements-forms}

[!DNL Experience Manager] 6.5 O Service Pack 7 do Forms melhora o desempenho para:

* Validação dos valores de campo no servidor ao enviar um formulário adaptável.

* Converter um formulário PDF em um formulário adaptável usando o [!DNL Automated Forms Conversion service].

#### Suporte para grupos de disponibilidade Always On do Microsoft SQL Server 2016 para Alta Disponibilidade (6.5.7.0) {#always-on-availability-groups}

[!DNL Experience Manager Forms] O agora oferece suporte aos grupos de disponibilidade Always On do  [!DNL Microsoft] SQL Server 2016 para implantações de OSGi com Alta Disponibilidade.

#### Modelo de dados de formulário Configuração do cliente HTTP para otimizar o desempenho (6.5.7.0) {#fdm-http-client-config}

[!DNL Experience Manager Forms] O modelo de dados de formulário ao integrar com serviços da Web RESTful como fonte de dados agora inclui configurações de cliente HTTP para otimização de desempenho. Consulte [Configurar fontes de dados](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration).

#### Disponibilidade da opção de redefinição para cada componente no modo Layout (6.5.7.0) {#reset-option-layout-mode}

Agora é possível usar a opção de redefinição para cada componente no modo Layout de um formulário adaptável. Ao definir um layout de várias colunas para um painel, você pode usar esse recurso para redefinir componentes individuais dentro do painel. Consulte [Usar o modo de layout para redimensionar componentes](../../help/forms/using/resize-using-layout-mode.md#resize-components).

#### Preencha previamente um formulário adaptável no cliente (6.5.6.0) {#prefill-merge-data-at-client}

Ao preencher previamente um formulário adaptável, o servidor [!DNL Experience Manager Forms] une os dados a um formulário adaptável e entrega o formulário preenchido a você. Por padrão, a ação de mesclagem de dados ocorre no servidor.
Agora você pode configurar o servidor [!DNL Experience Manager Forms] para [executar a ação de mesclagem de dados no cliente](../../help/forms/using/prepopulate-adaptive-form-fields.md) em vez do servidor. Reduz significativamente o tempo necessário para preencher e renderizar formulários adaptáveis.

#### Integração do modelo de dados de formulário com APIs RESTful em um servidor com implementação SSL bidirecional (6.5.6.0) {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] O modelo de dados de formulário agora pode ser  [integrado com RESTful APIs em um servidor que tem um SSL bidirecional implementado nele](../../help/forms/using/configure-data-sources.md).

#### Adição de suporte para [!DNL Adobe Sign] Tags de texto no Automated forms conversion Service (6.5.6.0) {#sign-integration-acroform-afcs}

Se um AcroForm incluir [!DNL Adobe Sign] Tags de texto, esses campos agora serão reconhecidos e representados como campos [!DNL Adobe Sign] no formulário adaptável convertido usando [!DNL Automated Forms Conversion service]. Um assinante pode preencher esses campos ao assinar o formulário adaptável.

#### Suporte para converter PDF forms coloridos em formulários adaptáveis (6.5.6.0) {#colored-PDF-forms}

Você pode usar [!DNL Automated Forms Conversion service] para converter PDF forms coloridos em formulários adaptáveis.

#### Suporte para protocolos SMB 2 e SMB 3 (6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] agora suporta protocolos SMB 2 e SMB 3.

#### Armazenamento em cache aprimorado para páginas de formulário adaptável traduzidas (6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

Agora é possível especificar [locale como um seletor no URL do formulário adaptável, em vez de um argumento no URL do formulário adaptável](../../help/forms/using/supporting-new-language-localization.md). Ajuda a colocar formulários adaptáveis em cache em [!DNL Experience Manager Dispatcher]. O armazenamento em cache de formulários adaptáveis traduzidos não era possível em versões anteriores. Para obter informações detalhadas sobre como configurar o armazenamento em cache para usar o local como seletor no URL do formulário adaptável, consulte [Configurar o cache do formulário adaptável no dispatcher](../../help/forms/using/configure-adaptive-forms-cache.md).

#### Salve a saída do serviço de modelo de dados de formulário em uma variável (6.5.6.0) {#save-fdm-service-to-variable}

O modelo de dados de formulário permite salvar a saída de um serviço de modelo de dados de formulário em uma variável. [!DNL Experience Manager Forms] agora mapeia automaticamente o tipo de serviço de modelo de dados de formulário para o tipo de variável.

#### Anexar vários arquivos para o componente Anexo de arquivo (6.5.6.0) {#attach-multiple-files}

Agora é possível [anexar vários arquivos](../../help/forms/using/introduction-forms-authoring.md) ao componente [!UICONTROL Anexo de arquivo] de formulários adaptáveis.

#### Personalizar as colunas da Caixa de entrada do Adobe Experience Manager (6.5.5.0) {#customize-aem-inbox-columns}

Você pode personalizar uma [!DNL Experience Manager] Caixa de entrada para alterar o título padrão de uma coluna, reorganizar a posição de uma coluna e exibir colunas adicionais com base nos dados de um fluxo de trabalho. Os membros do grupo `administrators` ou `workflow-administrators` podem personalizar as colunas. Para obter mais informações, consulte [Admin Control](../sites-authoring/inbox.md#inbox-admin-control).

![Personalizar colunas da Caixa de entrada do Experience Manager](assets/customize-columns.gif)

#### Salvar comunicações interativas como rascunho (6.5.5.0) {#save-as-draft}

Você pode usar a interface do usuário do agente para salvar um ou mais rascunhos de cada Comunicação interativa e recuperar o rascunho posteriormente para continuar trabalhando nela. Você pode especificar um nome diferente para cada rascunho para identificá-lo. Para obter mais informações, consulte [Salvar comunicações interativas como rascunho](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![Salvar como rascunho](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] suporte ao servidor de aplicativos (6.5.5.0)  {#weblogic-support}

A Adobe Experience Manager Forms adicionou suporte para [!DNL Oracle WebLogic 12] para Adobe Experience Manager Forms no JEE. Você pode atualizar de uma versão anterior ou configurar um novo Experience Manager 6.5 Forms no servidor JEE em [!DNL Oracle WebLogic] 12.2.1.4 e posterior. Mais tarde corresponde às alterações de versão secundária, onde x em 12.2.1.x é substituído por um número de versão.

#### Melhorias de acessibilidade (6.5.5.0) {#accessibility-improvements}

O Adobe Experience Manager Forms inclui os seguintes aprimoramentos de acessibilidade:

* Quando um usuário visualiza um formulário adaptável como um formulário HTML, o campo [!UICONTROL Assinatura do rabisco] retém o foco da guia.

* As mensagens de erro exibidas ao enviar um formulário adaptável agora contêm o atributo `aria-describedBy`. O atributo é anexado aos campos mencionados na mensagem de erro. O atributo `aria-describedby` indica as IDs dos elementos que descrevem o objeto. Ajuda a estabelecer uma relação entre widgets ou grupos e texto que os descreveu.

* Se um formulário adaptável tiver alguns campos obrigatórios, o atributo obrigatório será definido como `True` para esses campos no schema de acessibilidade ARIA.

#### Autenticação com certificado X-509 para serviços da Web baseados em SOAP no modelo de dados de formulário (6.5.5.0) {#x509-based-authentication-soap}

O modelo de dados de formulário agora oferece suporte à autenticação baseada em certificado X-509 ao usar serviços da Web SOAP como a fonte de dados. Para obter mais informações, consulte [Configurar serviços Web SOAP](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### Outras melhorias importantes (6.5.5.0) {#other-improvements}

* Experience Manager 6.5 Forms na Segurança de documentos JEE agora é baseado em [!DNL Apache Struts 2].

* Adição de suporte para [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### Gerar saída para impressão em workflows do Experience Manager Forms (6.5.4.0) {#generate-printable-output}

A etapa de fluxo de trabalho Gerar saída para impressão permite integrar um arquivo de modelo de origem a um arquivo de dados. Essa integração permite que você imprima ou salve cópias diferentes do arquivo de modelo. A etapa gera uma saída PCL, PostScript, ZPL, IPL, TPCL ou DPL. Para obter mais informações sobre esse recurso, consulte [Fluxo de trabalho centrado no Forms em OSGi - Referência da etapa](../forms/using/aem-forms-workflow-step-reference.md).

![Gerar saída para impressão](assets/generate-print-output-step.gif)

#### Suporte a várias colunas para formulários adaptáveis e comunicações interativas no modo Layout (6.5.4.0) {#multi-column-adaptive-forms}

Agora é possível definir o número de colunas para um painel em formulários adaptáveis e comunicações interativas. Alterne para o modo de layout para usar a nova opção de várias colunas. Para obter mais informações, consulte [Usar o modo Layout para redimensionar componentes](../forms/using/resize-using-layout-mode.md).

![Layout de várias colunas](assets/multi-column-layout.gif)

#### Personalizações da Caixa de entrada do Experience Manager (6.5.4.0) {#aem-inbox}

A nova opção Controle de administrador permite que os administradores:

* Personalize o texto e o logotipo do cabeçalho.

* Controlar a exibição de links de navegação disponíveis no cabeçalho.

A opção Controle de administrador é visível somente para os membros do grupo `administrators` ou `workflow-administrators`. Para obter mais informações sobre esse recurso, consulte [Sua Caixa de entrada](../sites-authoring/inbox.md).

#### Suporte a rich text em formulários HTML5 (6.5.4.0) {#rich-text-support}

Converta um campo de texto em um formulário XFA em um campo de rich text em um formulário HTML5. Para obter mais informações, consulte [Criação de modelos de formulário para formulários HTML5](../forms/using/designing-form-template.md).

#### Aprimoramentos de acessibilidade (6.5.4.0) {#forms-accessibility-enhancements-6540}

O Experience Manager Forms inclui os seguintes aprimoramentos de acessibilidade:

* Os leitores de tela anunciam as caixas de seleção, os links, o Seletor de data e os campos de Entrada de data corretamente em um formulário adaptável.

* Cada página de um formulário adaptável agora inclui um título e um rótulo principal de marca.

#### Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário do Experience Manager Forms (6.5.3.0) {#share-request-access}

Você pode compartilhar seus itens da Caixa de entrada com outro usuário. Assim que outro usuário tiver acesso aos itens da Caixa de entrada, ele poderá reivindicar e tomar as medidas apropriadas nos itens compartilhados. Da mesma forma, você pode solicitar acesso aos itens da Caixa de entrada de outros usuários. Consulte [Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário](../forms/using/configure-shared-queues-osgi.md).

#### Defina as configurações de ausência do escritório para os itens da Caixa de entrada de um usuário do Experience Manager Forms (6.5.3.0) {#configure-out-of-office}

Se você planeja estar fora do escritório, você pode especificar o que acontece com os itens que são atribuídos a você para esse período.
Você tem a opção de especificar uma data e hora de início e uma data e hora de término para que as configurações de ausência do escritório entrem em vigor. Você pode definir uma pessoa padrão para a qual todos os itens são enviados. Consulte [Definir configurações de ausência do escritório](../forms/using/configure-out-of-office-settings.md).

#### Gere várias comunicações interativas usando a API em lote para o Experience Manager Forms (6.5.3.0) {#generate-multiple-ic}

Você pode usar a API em lote para produzir várias comunicações interativas de um modelo. O modelo é uma comunicação interativa sem dados. A API em lote combina dados com um modelo para produzir uma comunicação interativa. A API é útil na produção em massa de comunicações interativas. Por exemplo, contas telefônicas, demonstrativos de cartão de crédito para vários clientes. Consulte [Gerar várias comunicações interativas usando a API em lote](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

<!-- TBD: Check if the wider team released anything in FY21.
-->

## Versões de chave desde [!DNL Adobe Experience Manager] 6.5 SP8 {#key-releases-since-last-sp}

Entre 25 de fevereiro de 2021 e 27 de maio de 2021, o Adobe lançou o seguinte, além dos Service Packs:

* [!DNL Adobe Experience Manager] como Cloud Service  [2021.2.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-2-0.html),  [2021.3.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-3-0.html) e  [2021.4.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=en#release-date).

* [[!DNL Experience Manager] aplicativo de desktop 2.1 (2.1.2.0)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Experience Manager Screens: Feature Pack 202103](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202103.html?lang=en)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] Documentação 6.5](../user-guide/home.md)
* [Notas de versão gerais para [!DNL Adobe Experience Manager] 6.5](release-notes.md)
* [Notas de versão do Service Pack para [!DNL Adobe Experience Manager] 6.5](sp-release-notes.md)

