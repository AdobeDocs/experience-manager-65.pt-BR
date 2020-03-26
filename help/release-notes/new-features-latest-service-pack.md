---
title: Novidades do Adobe Experience Manager 6.5 Service Pack 4
description: Novidades do Adobe Experience Manager 6.5 Service Pack 4
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 61d1531c020b5a25207b5e3f1c2b0c14e2974e02

---


# Novidades do Adobe Experience Manager 6.5 Service Pack 4 {#aem-whats-new-service-pack-4}

O Adobe Experience Manager (AEM) 6.5 oferece recursos e melhorias contínuas por meio de Service Packs trimestrais. A abordagem o beneficia à medida que as inovações se tornam mais fáceis de adotar.

O AEM Service Pack 4 (6.5.4.0) foi lançado em 5 **de março de 2020**. Este artigo destaca os principais recursos da oferta 6.5 Service Packs para tornar sua jornada do AEM mais enriquecedora.

## AEM Sites {#aem-sites}

### Aprimoramentos do Sistema de estilo

Agora é possível selecionar estilos na caixa de diálogo do componente usando o Sistema de estilo aprimorado.

### Melhorias no desempenho em várias áreas {#performance-improvements}

* Redução do tempo para carregar e inicializar o ContextHub em um site (`contexthub.kernel.js`). Isso resulta em cargas de página mais rápidas durante uma visita ao site.

* Redução do tempo para atualizar uma página depois de arrastar Fragmentos de experiência para o Editor de páginas de sites.

* Tempo de carregamento reduzido para entradas em uma página Sites com mais de 200 cópias online na Visão geral **** da Live Copy.

* Funcionamento aprimorado de URLs incompletos ou inválidos. Tais URLs podem retardar o Editor de modelos.

## Ativos AEM {#aem-assets}

### Configurar ativos AEM com o Portal de marcas {#configure-assets-bp}

O canal de autorização entre os ativos AEM e o Portal de marcas foi alterado. Anteriormente, o Brand Portal estava configurado na interface clássica via Gateway OAuth herdado, que usa a troca de token JWT para obter um Token de acesso IMS para autorização. Os ativos AEM agora estão configurados com o Portal de marcas por meio da E/S da Adobe, que obtém um token IMS para autorização do locatário do Portal de marcas.

As etapas para configurar os ativos AEM com o Brand Portal são diferentes dependendo da versão do AEM e se você está configurando pela primeira vez ou atualizando as configurações existentes. Consulte [Configurar ativos AEM com o Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) da marca para obter detalhes.


### Accessibility enhancements {#accessibility-enhancements}

Os ativos do Experience Manager incluem os seguintes aprimoramentos de acessibilidade:

* Teclas de seta no teclado podem ser usadas para mover e deslocar áreas em imagens ampliadas. Para obter mais informações, consulte [pré-visualizações usando apenas](../assets/managing-assets-touch-ui.md#previewing-assets)teclas de teclado.

* As caixas de seleção de estado misto (nas quais, a menos que você marque todos os predicados aninhados, as caixas de seleção de primeiro nível não serão selecionadas e passarão por elas) no painel Filtros poderão ser lidas pelos leitores de tela.

* As restrições de formato de data e hora são fornecidas nos rótulos de campo dos campos de data, para permitir que os usuários digitem a data no formato correto usando o teclado.

   Por exemplo, `On Time (MM-DD-YYYY HH:mm)`. Aqui MM é mês em formato de dois dígitos, AAAA é ano, DD é dia em formato de dois dígitos, HH é hora em formato militar de 24 horas e mm é minuto.

* O `X` símbolo no botão para remover as tags atualmente selecionadas agora é anunciado pelos leitores de tela, juntamente com o número de tags selecionadas.

## Formulários AEM {#aem-forms}

### Gerar saída imprimível em workflows do AEM Forms {#generate-printable-output}

A etapa de fluxo de trabalho Gerar saída imprimível permite integrar um arquivo de modelo de origem a um arquivo de dados. Essa integração permite que você imprima ou salve cópias diferentes do arquivo de modelo. A etapa gera uma saída PCL, PostScript, ZPL, IPL, TPCL ou DPL. Para obter mais informações sobre esse recurso, consulte Fluxo de trabalho centrado no [Forms em OSGi - Referência](../forms/using/aem-forms-workflow-step-reference.md)de etapas.

![Gerar saída para impressão](assets/generate-print-output-step.gif)

### Suporte a várias colunas para formulários adaptáveis e comunicações interativas no modo Layout {#multi-column-adaptive-forms}

Agora é possível definir o número de colunas para um painel em formulários adaptáveis e comunicações interativas. Alterne para o modo de layout para usar a nova opção de várias colunas. Para obter mais informações, consulte [Usar o modo Layout para redimensionar componentes](../forms/using/resize-using-layout-mode.md).

![Layout de várias colunas](assets/multi-column-layout.gif)

### Personalizações da Caixa de entrada do AEM {#aem-inbox}

A nova opção Controle de administrador permite que os administradores:

* Personalizar o texto e o logotipo do cabeçalho

* Controlar a exibição de links de navegação disponíveis no cabeçalho

A opção Controle de administrador está visível somente para os membros do grupo de administradores ou administradores de fluxo de trabalho. Para obter mais informações sobre esse recurso, consulte [Sua Caixa de entrada](../sites-authoring/inbox.md).

### Suporte a Rich Text em formulários HTML5 {#rich-text-support}

Converta um campo de texto em um formulário XFA em um campo de texto formatado em um formulário HTML5. Para obter mais informações, consulte [Criar modelos de formulário para formulários](../forms/using/designing-form-template.md)HTML5.

### Accessibility enhancements {#forms-accessibility-enhancements-6540}

O Experience Manager Forms inclui os seguintes aprimoramentos de acessibilidade:

* Os leitores de tela anunciam as caixas de seleção, os links, o Seletor de data e os campos de Entrada de data corretamente em um formulário adaptável.

* Cada página de um formulário adaptável agora inclui um título e um rótulo principal.

## Principais recursos dos Service Packs anteriores do AEM 6.5

### Imagem inteligente para Dynamic Media (6.5.3.0) {#smart-imaging}

A geração de imagens inteligentes usa as características de exibição exclusivas de cada usuário para fornecer automaticamente as imagens certas, otimizadas para sua experiência, resultando em melhor desempenho e envolvimento. A geração de imagens inteligentes funciona com as predefinições de imagens existentes e usa inteligência no último milissegundo do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte Imagem [inteligente](../assets/imaging-faq.md).

### Pesquisa visual para AEM Assets (6.5.2.0) {#visual-search}

Os usuários do Assets podem pesquisar imagens visualmente semelhantes. O AEM exibe as imagens com tags inteligentes do repositório DAM que são semelhantes a uma imagem selecionada pelo usuário. See [Visual search](../assets/search-assets.md).

### Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário do AEM Forms (6.5.3.0) {#share-request-access}

Você pode compartilhar seus itens da Caixa de entrada com outro usuário. Quando outro usuário tiver acesso aos itens da Caixa de entrada, ele poderá solicitar e tomar as medidas apropriadas nos itens compartilhados. Da mesma forma, você pode solicitar acesso a itens da Caixa de entrada de outros usuários. Consulte [Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário](../forms/using/configure-shared-queues-osgi.md).

### Defina as configurações de disponibilidade para itens da Caixa de entrada de um usuário do AEM Forms (6.5.3.0) {#configure-out-of-office}

Se planeja estar fora do escritório, você pode especificar o que acontece com os itens que lhe são atribuídos para esse período.
Você tem a opção de especificar uma data e hora de start e uma data e hora de término para que suas configurações de fora do escritório entrem em vigor. Você pode definir uma pessoa padrão para a qual todos os itens serão enviados. Consulte [Configurar configurações](../forms/using/configure-out-of-office-settings.md)fora do escritório.

### Gerar várias comunicações interativas usando a API de lote para AEM Forms (6.5.3.0) {#generate-multiple-ic}

Você pode usar a API de lote para produzir várias comunicações interativas a partir de um modelo. O modelo é uma comunicação interativa sem dados. A API de lote combina dados com um modelo para produzir uma comunicação interativa. A API é útil na produção em massa de comunicações interativas. Por exemplo, contas telefônicas, declarações de cartão de crédito para vários clientes. Consulte [Gerar várias comunicações interativas usando a API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)de lote.

## Versões de chave desde o AEM 6.5 SP3

Entre 12 de dezembro de 2019 e 5 de março de 2020, a Adobe lançou os seguintes recursos que estão fora do principal produto do AEM:

* AEM Cloud Manager 2020.1.0 e 2020.2.0

   Melhore o status do pipeline e a capacidade de baixar registros para várias etapas. Consulte:

   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)


   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-2-0.html)


* Atualizações da CLI do AEM Cloud Manager

   Automatize tarefas do Cloud Manager usando a ferramenta de linha de comando. Consulte [GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases).

* AEM Sites: Tipo de Arquivo do Projeto 23

   A melhor maneira de start de um novo projeto do AEM. O Archetype 23 mescla o [Project Archetype para SPA e os sites regulares em um único](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23) e fornece um tema padrão para lançar o start do seu desenvolvimento de front-end.

* AEM Sites: Site de referência WKND

   [Novo projeto](https://www.wknd.site/) de referência repleto de práticas recomendadas sobre como criar sites com o AEM. Saiba mais lendo o tutorial [atualizado do](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)WKND. Você pode obter o código mais recente do [GitHub](https://github.com/adobe/aem-guides-wknd/releases).

* AEM Sites: Commerce CIF Core Components 0.7.0 e 0.9.0

   Integre o AEM Sites ao Magento Commerce. Consulte [estendendo componentes principais e arquétipo de projeto dedicados com foco em Comércio](https://github.com/adobe/aem-core-cif-components/releases).

* AEM Assets: Aplicativo para desktop 2.0.1.1

   Consulte [Obter acesso ao desktop para os ativos](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html).

* AEM Screens: Feature Pack 202001

   Sinalização digital diretamente do AEM. Instale as melhorias com o Feature Pack mais recente para [permitir a reprodução síncrona em vários players](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)de mídia.

## Recursos úteis

* [Guias do usuário do AEM 6.5](../user-guide/home.md)

* [Notas de versão gerais do Adobe Experience Manager 6.5](release-notes.md)

* [Notas de versão do Service Pack para o Adobe Experience Manager 6.5](sp-release-notes.md)
