---
title: Recursos e aprimoramentos principais cumulativos na versão Adobe Experience Manager 6.5.
description: Uma lista cumulativa dos principais recursos e aprimoramentos feitos no Adobe Experience Manager 6.5 em relação às oito versões anteriores do service pack.
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: 03c070f7bba1d66ce2a5309d2ab79567dbef3264
workflow-type: tm+mt
source-wordcount: '3539'
ht-degree: 6%

---

# Principais recursos e aprimoramentos cumulativos

Uma lista cumulativa dos principais recursos e aprimoramentos do Adobe Experience Manager 6.5 para versões anteriores do service pack.

Consulte também [Notas de versão mais recentes do Service Pack do Adobe Experience Manager 6.5](/help/release-notes/release-notes.md).


## AEM 6.5, Service Pack 23 — 22 de maio de 2025

### Forms {#forms-sp23}

* [Hiperlinks acessíveis com estilo de texto misto em PDFs estáticos](https://helpx.adobe.com/content/dam/help/pt-br/experience-manager/6-5/forms/pdf/using-designer.pdf): os hiperlinks que contêm estilos de texto misto em PDFs estáticos agora são marcados como um único elemento acessível. Esse aprimoramento simplifica a estrutura da árvore de tags, melhora a navegação do leitor de tela e oferece suporte a uma melhor conformidade com acessibilidade.

* [Matriz de Plataforma com Suporte Atualizada](/help/forms/using/aem-forms-jee-supported-platforms.md)

  A versão mais recente apresenta atualizações na matriz de plataformas compatíveis, garantindo a compatibilidade com as tecnologias mais recentes.

   * Cliente do gerenciador de conteúdo IBM® 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Driver JDBC do Microsoft® SQL Server 12.8

   * Red Hat® Enterprise Linux® 9 (Kernel 4.x, 64 bits)

* [Componente de anexo de arquivo protegido](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment): como medida de segurança, o componente agora impede o envio de arquivos com extensões modificadas que tentam ignorar as verificações de tipo de arquivo permitidas. Esses arquivos são bloqueados durante o envio para garantir que somente tipos de arquivos válidos sejam aceitos.

## AEM 6.5, Service Pack 22 — 21 de novembro de 2024

### Sites {#sites}

[O Universal Editor](/help/sites-developing/universal-editor/introduction.md) agora está disponível no AEM 6.5 para casos de uso headless com o aplicativo de um pacote de recursos.

### [!DNL Assets]

A guia IPTC agora oferece suporte aos campos de texto [!UICONTROL Texto Alt] e [!UICONTROL Descrição Estendida]. (Assets-34918)

### Forms {#forms-sp22}

#### Novos recursos do GA no AEM Forms {#ga-aem-forms-sp22}

* Adição de suporte para habilitar a incorporação de fontes nas [APIs em lote de comunicações interativas](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel) - As Comunicações interativas agora incluem suporte para a incorporação de fontes do Adobe Ming e do Adobe Myungjo em PDFs gerados por meio da API em lote. Esse aprimoramento garante a renderização de texto preciso em documentos gerados, mesmo ao usar subconjuntos de fontes, fornecendo suporte aprimorado para conteúdo multilíngue em saídas do PDF.

* [API de índice para acessibilidade do PDF](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api) - O AEM Forms no OSGi agora oferece suporte à nova API de marca de índice para aprimorar o PDF para padrões de acessibilidade. Ele torna os PDFs mais acessíveis para usuários com tecnologia assistiva.

* [Resolução XDP de fragmento](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository) - O AEM Forms no OSGi agora resolve XDPs de fragmento referenciados em XDPs primários e armazenados no Repositório CRX do AEM.

* [Aprimoramentos de conformidade com o PDF/A](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents) - Agora os usuários podem converter PDFs para formatos PDF/A (1a, 2a, 3a) para fins de arquivamento, garantindo a acessibilidade e verificando a conformidade com esses padrões.

* **Suporte para dimensionamento automático de fontes para documentos estáticos do PDF** - AEM Forms Designer, OutputService e FormsService agora oferecem suporte para dimensionamento automático de fontes para PDFs estáticos. Se o usuário definir o tamanho da fonte 0 para campos de texto, numérico, de senha ou de data e hora, o tamanho da fonte será ajustado automaticamente nesses campos sem alterar o tamanho geral do campo. Para usar o recurso, os usuários passam um sinalizador no XCI personalizado: `<behaviorOverride>patch-LC-3921991:1</behaviorOverride>`.

#### Novos recursos do Beta no AEM Forms {#beta-aem-forms-sp22}

O recurso beta oferece uma oportunidade única para obter acesso exclusivo a inovações de última geração e ajudar a moldar seu desenvolvimento. Interessado em ativar um recurso beta para seus ambientes? Envie um email de seu endereço oficial para aem-forms-ea@adobe.com com a lista de recursos nos quais você está interessado.

* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md) e [serviços CAPTCHA de Cupons de Turnstile](/help/forms/using/integrate-adaptive-forms-turnstile.md): o AEM Forms oferece suporte aos seguintes serviços Captcha:
   * O Captcha protege os formulários contra bots, spam e abuso automatizado, desafiando os usuários com um widget de caixa de seleção. Ele garante que apenas os usuários humanos prossigam, melhorando a segurança das transações on-line.
   * O Cloudflare Turnstile oferece uma medida de segurança que visa proteger formulários contra bots automatizados, ataques mal-intencionados, spams e tráfego automatizado indesejado. Ele apresenta uma caixa de seleção no envio do formulário para verificar se ele é humano, antes de permitir que ele envie o formulário.

* Versão do formulário adaptável:
   * [Criar várias versões de um Formulário adaptável](/help/forms/using/add-versioning-reviews-comments.md) - Agora os usuários podem gerenciar facilmente variações de formulários existentes. Esse processo simplifica o controle de versões e facilita a comparação para a otimização de formulários, tudo em um único fluxo de trabalho simplificado.
   * [Comparar Forms Adaptável](/help/forms/using/compare-forms-core-components.md): agora os usuários podem facilmente comparar dois formulários para identificar diferenças. Ele facilita a colaboração perfeita, permitindo que os membros da equipe comparem revisões e discutam alterações com eficiência.

## AEM 6.5, Service Pack 21 — 6 de junho de 2024

### [!DNL Assets]

#### Aprimoramentos

A guia IPTC agora oferece suporte aos campos de texto [!UICONTROL Texto Alt] e [!UICONTROL Descrição Estendida]. (Assets-34918)

#### Acessibilidade

* Se o status de processamento de um ativo for Falha ou Metadados falharam, as legendas e a interface de rastreamento de áudio agora funcionam adequadamente. (Assets-37281)
* Ao salvar um metadado de ativo e tentar editá-lo, o nome do idioma agora é exibido. (Assets-37281)

### [!DNL Forms]

Alguns dos principais recursos e aprimoramentos desta versão incluem:

* **Suporte para Credenciais Oauth**: uma credencial nova e mais fácil de usar para autenticação de servidor para servidor, substituindo a credencial de Conta de Serviço (JWT) existente. (NPR-41994)
* [Aprimoramentos do Editor de regras no AEM Forms](/help/forms/using/rule-editor-core-components.md):
   * Suporte para implementar condições aninhadas com funcionalidade `When-then-else`.
   * Validar ou redefinir painéis e formulários, incluindo campos.
   * Suporte para recursos modernos do JavaScript, como funções de seta e esquerda (suporte para ES10) nas Funções personalizadas.
* [API de Marca Automática para Acessibilidade do PDF](/help/forms/using/aem-document-services-programmatically.md#doc-utility-services-doc-utility-services): o AEM Forms no OSGi agora oferece suporte à nova API de Marca Automática para aprimorar o PDF para padrões de acessibilidade, adicionando marcas: parágrafos e listas. Ele torna os PDFs mais acessíveis para usuários com tecnologia assistiva.
* **Suporte a PNG de 16 bits**: o serviço ImageToPdf da PDF Generator agora oferece suporte à conversão de PNGs com intensidade de cor de 16 bits.
* **Aplicar artefatos a blocos de texto individuais em XDPs**: o Forms Designer agora permite que os usuários definam configurações em blocos de texto individuais em arquivos XDP. Essa capacidade permite controlar os elementos que são tratados como artefatos nos PDFs resultantes. Esses elementos, como cabeçalhos e rodapés, são acessíveis para as tecnologias assistivas. Os principais recursos incluem marcar blocos de texto como artefatos e incorporar essas configurações nos metadados XDP. O serviço de saída do Forms aplica essas configurações durante a geração do PDF, garantindo a marcação adequada do PDF/UA.
* **O AEM Forms Designer é certificado com o `GB18030:2022` padrão**: com a certificação `GB18030:2022`, agora o Forms Designer oferece suporte ao conjunto de caracteres Unicode chinês que permite inserir caracteres chineses em todos os campos editáveis e caixas de diálogo.
* [O suporte para WebToPDF route no JEE Server](/help/forms/using/admin-help/configure-service-settings.md#generate-pdf-service-settings-generate-pdf-service-settings) usando o serviço PDF Generator agora oferece suporte para WebToPDF route para conversão de arquivos HTML em documentos PDF em JEE. Esse suporte complementa as rotas Webkit e WebCapture (somente Windows) existentes. Embora a rota WebToPDF já esteja disponível no OSGi e seja estendida para JEE. Agora, nas plataformas JEE e OSGi, o serviço PDF Generator é compatível com as seguintes rotas em diferentes sistemas operacionais:
   * **Windows**: Webkit, WebCapture, WebToPDF
   * **Linux®**: Webkit, WebToPDF


## AEM 6.5, Service Pack 20 — 22 de fevereiro de 2024

### [!DNL Assets]

* O Dynamic Media agora é compatível com o formato de imagem HEIC sem perdas para Apple iOS/iPadOS. Consulte [fmt](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt) na API de disponibilização e renderização de imagens do Dynamic Media.
* O Gerenciador de vários sites (MSM) agora é compatível com estruturas de Fragmento de experiência, incluindo pastas e subpastas, para a implantação eficiente em massa de Fragmentos de experiência em Live Copies.

### [!DNL Forms]

* **Relatório de transações no AEM Forms em JEE**: o recurso de relatório de transações foi introduzido para o AEM Forms em JEE. Ele permite o registro abrangente de transações de documentos, como Conversões, Representações e Envios. Esse aprimoramento aumenta a eficiência e facilita uma melhor manutenção de registros. O recurso está desativado por padrão. Você pode ativá-lo na interface do usuário do administrador.
* **Segurança aprimorada com suporte para ECDSA**: a AEM Forms agora oferece suporte robusto para o ECDSA (Elliptic Curve Digital Signature Algorithm) nas pilhas JEE e OSGi. Os usuários agora podem Assinar, Certificar e Verificar documentos do PDF com segurança avançada. Os algoritmos de curva EC compatíveis incluem:
   * Curva elíptica ECDSA P256 com algoritmo de resumo SHA256
   * Curva elíptica ECDSA P384 com algoritmo de compilação SHA384
   * Curva elíptica ECDSA P512 com algoritmo de compilação SHA512
* **Compatibilidade perfeita com o Windows 11 para Forms Designer**: o AEM Forms Designer agora oferece suporte ao Windows 11, garantindo instalação e operação ininterruptas. Os usuários podem atualizar com confiança para o Windows 11 sem o incômodo de reinstalar o Forms Designer ou se preocupar com problemas de compatibilidade, garantindo um fluxo de trabalho ininterrupto.
* **Acessibilidade aprimorada com a função personalizada &quot;Legenda&quot; no AEM Forms Designer**: o AEM Forms Designer agora inclui uma função personalizada de acessibilidade chamada &quot;Legenda&quot;, permitindo que os usuários criem XDPs com elementos personalizados de legenda. Esse recurso melhora a acessibilidade ao permitir que os usuários integrem legendas personalizadas em seus designs de documento para que possam melhorar a inclusão e a experiência do usuário.

## AEM 6.5, Service Pack 19 — 7 de dezembro de 2023

* Ativação do usuário do Editor de páginas do Sites/Componente de imagem para fazer referência a ativos do Assets Cloud Service remoto. (SITES-13448, SITES-13433)
* O AEM agora é compatível com a classificação do lado do servidor para agilizar a navegação do projeto na exibição em lista. Os nós de projeto são classificados com base na coluna selecionada pelo usuário antes de aparecer na interface.

### [!DNL Forms]

* **Novos componentes principais do formulário adaptável**: guias Verticais, Termos e condições e Caixa de seleção são adicionados para aprimorar a escalabilidade dos formulários.
   * **[Componente de caixa de seleção](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox)**: o Forms adaptável baseado em Componentes principais agora pode incluir um componente de caixa de seleção. Permite que os usuários façam escolhas binárias, selecionando ou desmarcando uma opção específica. Normalmente, ela aparece como uma pequena caixa que pode ser clicada ou tocada para alternar entre dois estados: marcado e desmarcado. A caixa de seleção é um elemento de formulário comum usado para apresentar uma opção sim/não ou verdadeira/falsa.

   * **[Componente de Termos e Condições](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions)**: o Forms Adaptável baseado em Componentes Principais agora inclui um componente de Termos e Condições. Os autores de formulários adicionam esta seção para mostrar aos usuários os termos, condições ou contratos legais do serviço, produto ou plataforma. Esse componente foi projetado para informar os usuários sobre as regras, regulamentos e obrigações aos quais eles estão concordando ao enviar o formulário.

     ![Guias verticais, Termos e condições e componentes da Caixa de seleção](/help/forms/using/assets/forms-components.png)

   * **[Componente de guias verticais](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)**: o Forms adaptável baseado em Componentes principais agora pode organizar o conteúdo do formulário em uma lista vertical de guias, fornecendo um layout estruturado e navegável. Guias verticais em um formulário melhoram a experiência do usuário simplificando a navegação e organizando o conteúdo. Eles são especialmente úteis quando o formulário contém várias seções ou informações complexas.

* **[Versão de 64 bits do AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**: a versão de 64 bits do AEM Forms Designer oferece desempenho aprimorado, escalabilidade e gerenciamento de memória para potencializar sua experiência em criação de formulários. Com a arquitetura de 64 bits, você pode executar projetos ainda maiores e mais complexos com facilidade, garantindo fluxos de trabalho de design ininterruptos e eficiência otimizada. Aumente os recursos de design de formulários e abrace o futuro do AEM Forms Designer com esta versão de última geração.

* **[Conecte um Forms adaptável com a Lista do Microsoft® SharePoint](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**: o AEM Forms fornece uma integração pronta para uso para enviar dados de formulários diretamente para a Lista do SharePoint, permitindo que você use os recursos de Listas do SharePoint. Você pode configurar a Lista de SharePoint Microsoft® como uma fonte de dados para um Modelo de dados de formulário e usar a ação de envio Enviar usando Modelo de dados de formulário para conectar um Formulário adaptável à Lista de SharePoint.

* **[Suporte para configurar as propriedades do Documento de Registro para os Fragmentos do Formulário Adaptável](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**: agora é possível personalizar facilmente os fragmentos do Formulário Adaptável e seus campos no editor de Formulário Adaptável.

* **XMLFM de 64 bits**: a iteração de 64 bits do XMLFM apresenta desempenho aprimorado, escalabilidade e gerenciamento refinado de memória. É o primeiro serviço nativo de 64 bits implantado no lado do servidor. Ao utilizar sua capacidade inerente de acessar recursos de memória maiores em comparação ao seu equivalente de 32 bits, o XMLFM de 64 bits capacita o manuseio ininterrupto de cargas de trabalho de renderização maiores. Esse marco não só representa um salto no desempenho, como também introduz aprimoramentos importantes na estrutura de serviço nativa no AEM Forms Server. Essa atualização possibilita que o AEM Forms Server suporte qualquer serviço nativo de 64 bits com facilidade.

## AEM 6.5, Service Pack 18 — 24 de agosto de 2023

* Assets, Dynamic Media - [Suporte a várias legendas e faixas de áudio para vídeos no Dynamic Media](/help/assets/video.md#about-msma) — Agora é possível adicionar facilmente várias legendas e faixas de áudio a um vídeo principal. Esse recurso significa que os vídeos estão acessíveis a um público-alvo global. Você pode personalizar um único vídeo principal publicado para um público-alvo global em vários idiomas e seguir as diretrizes de acessibilidade para diferentes regiões geográficas. Os autores também podem gerenciar as legendas e faixas de áudio em uma única guia na interface do usuário do.
* Assets - Nos resultados da Pesquisa, agora é possível navegar até o local da pasta que contém um ativo para permitir que você execute várias tarefas de gerenciamento de ativos.
* O Seletor de polaris de sites em fragmentos de conteúdo melhorou o desempenho.
* Ativação do usuário do Editor de páginas do Sites/Componente de imagem para fazer referência a ativos do Assets Cloud Service remoto.
* Para encontrar um projeto na exibição em Lista rapidamente, onde você pode ter muitos projetos em seu sistema, o Adobe agora é compatível com a classificação do lado do servidor. Os nós de projeto são classificados no backend com base na coluna selecionada pelo usuário antes de renderizá-los na interface.
* O AEM 6.5.18.0 oferece suporte ao MongoDB 5.0 para 6.0.

### [!DNL Forms]

* **[Tratamento de erros aprimorado com manipuladores de erros personalizados no editor de regras](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms)** - Agora é possível invocar uma função personalizada (usando a Biblioteca do Cliente) em resposta a um erro retornado por um serviço externo. Além disso, você pode fornecer uma resposta personalizada aos usuários finais. Como alternativa, você pode realizar ações específicas para erros retornados por um serviço. Por exemplo, você pode chamar um fluxo de trabalho personalizado no backend para códigos de erro específicos ou informar ao cliente que o serviço está inativo

* **[Etapa aprimorada do fluxo de trabalho do Adobe Sign](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow-step-reference#sign-document-step)** - A etapa do fluxo de trabalho do Adobe Sign nos fluxos de trabalho do AEM está disponível com as seguintes melhorias.

   * **Segurança aprimorada com autenticação baseada em ID do governo para o Adobe Sign** - A autenticação baseada em ID do governo da Adobe Acrobat Sign oferece uma camada adicional de verificação. Ele permite aos usuários autenticar sua identidade usando IDs emitidas pelo governo (CNH, identificação nacional, passaporte). Ao usar documentos de identificação confiáveis, esse aprimoramento adiciona um nível extra de confiança ao processo de assinatura, tornando-o ideal para cenários que exigem maior segurança, conformidade e validação do usuário.

   * **Transparência aprimorada usando a Trilha de auditoria para documentos do Adobe Sign** - Use o recurso de Trilha de auditoria para obter insights detalhados sobre o ciclo de vida dos documentos do Adobe Sign. Com a Trilha de auditoria, agora é possível manter um registro abrangente de todas as ações e interações relacionadas aos documentos. Essas ações e interações incluem quem visualizou, editou ou assinou o documento, juntamente com carimbos de data e hora para cada evento. Esse aprimoramento é fundamental para manter a conformidade, resolver disputas e garantir a integridade de seus contratos digitais.


   * **As funções dos destinatários do Contrato foram estendidas além apenas do Signatário** - o Adobe Acrobat Sign permite que você expanda as funções dos destinatários do Contrato além apenas do Signatário, para melhor corresponder aos requisitos de fluxo de trabalho. Quando habilitado, cada recipient em um Contrato tem sua função configurável individualmente, sendo que Signatário é o padrão.


* **[Instalador completo do AEM Forms no JEE](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)** - O service pack traz um instalador completo do AEM Forms no JEE que oferece suporte para várias combinações de software novas, incluindo:
   * Microsoft® Windows Server 2022
   * Diretório ativo Microsoft® 2022
   * Oracle WebLogic 14C no Windows Server 2022
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * Conector JDBC do MySQL 8

Se você estiver instalando ou planejando usar o software mais recente para o ambiente AEM 6.5 Forms no JEE, a Adobe recomenda usar o instalador completo do AEM 6.5.18.0 Forms no JEE. Para explorar a lista completa de softwares recém-adicionados e obsoletos, consulte a documentação do AEM Forms no JEE ou do AEM Forms no OSGi.

## AEM 6.5, Service Pack 17 — 25 de maio de 2023

* **Melhorias na experiência de pesquisa**: agora você pode executar rapidamente as seguintes operações nos ativos exibidos nos resultados da pesquisa:
   * Criar um fluxo de trabalho
   * Criar uma versão
   * Criar ou remover relação de ativos

  Não é necessário navegar até o local do ativo e exibir suas propriedades para executar essas operações.

* **O _Instantâneo_**&#x200B;do Dynamic Media permite que você visualize modificadores de imagens e otimizações de Imagem Inteligente — como saída WebP ou AVIF, compactação com reconhecimento de largura de banda e dimensionamento de Proporção de Pixel de Dispositivo — usando imagens de teste ou URLs de Mídia Dinâmica. Você pode comparar imediatamente como cada configuração afeta a qualidade e o tamanho do arquivo.
Consulte [Instantâneo do Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot).
* **Streaming DASH com Dynamic Media** - Novo protocolo (DASH - Dynamic Adaptive Streaming por HTTP) iniciado para transmissão Adaptive Streaming na entrega de vídeo de Dynamic Media (com CMAF habilitado). Disponível agora para todas as regiões.
* **Integração do Experience Manager Sites e dos fragmentos de conteúdo com o Assets Next-Generation Dynamic Media** - Os usuários agora podem usar seus ativos hospedados na nuvem no Experience Manager Sites 6.5. Eles podem criar e entregar esses ativos em instâncias locais ou do Managed Services.

### [!DNL Forms]

* **[Forms adaptável no Editor de páginas do AEM](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)** - Agora você pode usar o Editor de páginas do AEM para criar e adicionar vários formulários às páginas dos sites rapidamente. Essa funcionalidade permite que os autores de conteúdo criem uma experiência perfeita para a captura de dados nas páginas de sites, usando o potencial dos componentes de formulários adaptáveis, incluindo comportamento dinâmico, validações, integração de dados, geração de documentos de registro e automação de processos empresariais. É possível:
   * Crie um formulário adaptável arrastando e soltando componentes de formulário no componente de Contêiner do Forms adaptável no editor do AEM Sites ou em Fragmentos de experiência.
   * Use o Assistente do Forms adaptável no editor do AEM Sites para criar formulários independentes de qualquer página do Sites, fornecendo a liberdade de reutilizar esses formulários em várias páginas.
   * Adicionar vários formulários a uma página de site, simplificando a experiência do usuário e fornecendo maior flexibilidade.
* **[Suporte ao reCAPTCHA Enterprise no Experience Manager Forms](/help/forms/using/captcha-adaptive-forms.md)** - Adição de suporte ao reCAPTCHA Enterprise no Experience Manager Forms. Essa capacidade oferece maior proteção contra atividades fraudulentas e spam, além do suporte existente ao Google reCAPTCHA v2.
* **[Adição de suporte para Adobe Acrobat Sign para o Governo com Experience Manager Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md)** - O AEM Forms agora se integra ao Adobe Acrobat Sign para o Governo (compatível com FedRAMP). Essa integração oferece um nível avançado de conformidade e segurança para assinaturas eletrônicas com envios de formulários adaptáveis para contas associadas ao governo (departamentos e agências governamentais). Integrações com o Adobe Acrobat Sign for Government permitem que parceiros e clientes governamentais da Adobe usem assinaturas eletrônicas no Adaptive Forms para algumas das linhas de negócios mais críticas e confidenciais. Essa camada adicional de segurança garante que todas as assinaturas eletrônicas sejam totalmente compatíveis com o nível moderado de conformidade do FedRAMP, proporcionando tranquilidade aos clientes governamentais da Adobe.
* **Habilitar a integração do Salesforce com o Experience Manager Forms para troca de dados** - Configure a integração entre o Experience Manager Forms e o aplicativo do Salesforce usando o fluxo de credenciais do cliente OAuth 2.0. Essa capacidade permite a autenticação e autorização diretas e seguras do aplicativo e permite uma comunicação perfeita sem o envolvimento do usuário.
* **Otimização e funcionalidade aprimorada do mecanismo de fluxo de trabalho**: aumente o desempenho dos mecanismos de fluxo de trabalho minimizando o número de instâncias de fluxo de trabalho. Além dos valores de status `COMPLETED` e `RUNNING`, o fluxo de trabalho também aceita três novos valores de status: `ABORTED`, `SUSPENDED` e `FAILED`.

## AEM 6.5, Service Pack 16 — 23 de fevereiro de 2023

Novo protocolo DASH (Dynamic Adaptive Streaming por HTTP) iniciado para transmissão de taxa de bits adaptável na entrega de vídeo do Dynamic Media (com CMAF [Common Media Application Format] habilitado).

* A transmissão adaptável (DASH/HLS) garante uma melhor experiência de visualização do usuário final para vídeos.
* DASH é o protocolo padrão internacional para transmissão de vídeo adaptável e é amplamente adotado no setor.
* Disponível agora na Ásia-Pacífico e na América do Norte; em breve na Europa-Oriente Médio-África.

### [!DNL Forms]

* [O Headless Adaptive Forms](https://experienceleague.adobe.com/en/docs/experience-manager-headless-adaptive-forms/using/overview) permite que seus desenvolvedores criem, publiquem e gerenciem formulários interativos que podem ser acessados e interagidos por meio de APIs, em vez de uma interface gráfica tradicional.

* [Os Componentes principais adaptáveis do Forms](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#features) são um conjunto de 24 componentes de código aberto compatíveis com BEM que são criados na base dos Componentes principais do WCM no Adobe Experience Manager. Esses componentes são de código aberto e fornecem aos desenvolvedores a capacidade de personalizar e estender esses componentes facilmente para atender às necessidades específicas de sua organização. Qualquer pessoa com habilidades existentes para personalizar [Componentes principais do WCM](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/get-started/authoring) pode personalizar e estilizar facilmente esses componentes.

* O serviço Reader Extension no OSGi agora fornece opções separadas para habilitar direitos de uso de importação e exportação em uma PDF para importar ou exportar dados no Adobe Acrobat Reader.

## AEM 6.5, Service Pack 15 — 24 de novembro de 2022

### [!DNL Forms]

* O AEM Forms Designer agora está disponível em [localidade em espanhol](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases).
* Agora você pode usar o [OAuth2 para autenticação com os protocolos de servidor de email do Microsoft® Office 365 (SMTP e IMAP)](/help/forms/using/oauth2-support-for-mail-service.md).
* Você pode definir a propriedade [Revalidar no servidor](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#enabling-server-side-validation-br) como verdadeira para identificar os campos ocultos para exclusão de um Documento de Registro no lado do servidor.
* O AEM Forms Designer requer uma versão de 32 bits do Visual C++ 2019 Redistributable (x86).

## AEM 6.5, Service Pack 14 — 25 de agosto de 2022

Somente correções de erros.

## AEM 6.5, Service Pack 13 — 26 de maio de 2022

* Usar CAPTCHA invisível em um formulário adaptável: agora é possível usar um CAPTCHA invisível para mostrar o desafio de CAPTCHA somente em caso de atividade suspeita. Se nenhuma atividade suspeita for encontrada, o desafio de CAPTCHA não será exibido. Isso ajuda a avaliar o preenchimento de formulários por humanos sem requisitos de caixa de seleção, reduz os esforços de personalização e melhora a experiência do usuário final.

* Adição de suporte para buscar cabeçalhos de resposta no pós-processador do modelo de dados de formulário para endpoints REST.

* Agora, ao gerar um arquivo de tradução do Formulário adaptável, a mesma sequência de textos no arquivo XLIFF gerado é idêntica à sequência de componentes no Formulário adaptável correspondente.

* Quando você localiza um Formulário adaptável e faz até mesmo uma pequena alteração no texto do idioma base, a tradução completa fica ausente para todos os outros idiomas. O problema foi corrigido em [!DNL Experience Manager] 6.5.13.0.

* Melhorias de acessibilidade para o Forms:

   * Adição de suporte para leitores de tela para reconhecer o cabeçalho e o corpo de uma tabela como entidades contínuas e conectadas. Isso ajuda os leitores de tela a navegar pelas tabelas corretamente. (NPR-37139)
   * Adição de suporte para leitores de tela para interromper a navegação no espaço de trabalho do HTML até que uma caixa de diálogo seja aberta.

## AEM 6.5, Service Pack 12 — 24 de fevereiro de 2022

* Após configurar uma conexão entre implantações remotas do DAM e do Sites, os ativos no DAM remoto são disponibilizados na implantação do Sites. Agora é possível executar as operações de atualização, exclusão, renomeação e movimentação nos ativos ou pastas remotos do DAM. As atualizações, com algum atraso, estão disponíveis automaticamente na implantação do Sites.
* Por padrão, agora, as implantações de push de uma origem de live copy para várias Live Copies são possíveis, sem exigir uma configuração de blueprint.
* O status das operações assíncronas em andamento agora é mostrado na interface para ajudar a impedir que os usuários acionem acidentalmente várias operações assíncronas no mesmo caminho.
* O suporte para autenticação baseada em IMS é fornecido para APIs do Analytics 2.0.
* Suporte de API para Fragmento de experiência do tipo oferta JSON.
* A solicitação de oferta agora é fornecida para a oferta de Exclusão (API do fragmento de experiência) no IMS.
* O repositório integrado (Apache Jackrabbit Oak) permanece na versão 1.22.9.
