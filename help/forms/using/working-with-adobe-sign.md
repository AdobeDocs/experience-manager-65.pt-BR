---
title: Usar o Adobe Sign em um formulário adaptável
seo-title: Usar o Adobe Sign em um formulário adaptável
description: Ative os fluxos de trabalho de assinatura eletrônica (Adobe Sign) para um formulário adaptável para automatizar os fluxos de trabalho de assinatura, simplificar os processos de assinatura única e múltipla e assinar eletronicamente formulários de dispositivos móveis.
seo-description: Ative os fluxos de trabalho de assinatura eletrônica (Adobe Sign) para um formulário adaptável para automatizar os fluxos de trabalho de assinatura, simplificar os processos de assinatura única e múltipla e assinar eletronicamente formulários de dispositivos móveis.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
translation-type: tm+mt
source-git-commit: 14975f409a0e17183b3da6bdc5a42c8073080108

---


# Usar o Adobe Sign em um formulário adaptável{#using-adobe-sign-in-an-adaptive-form}

O Adobe Sign permite fluxos de trabalho de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os fluxos de trabalho para processar documentos para áreas legais, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e outras.

Em um cenário típico de formulários adaptáveis e do Adobe Sign, um usuário preenche um formulário adaptável para solicitar um serviço. Por exemplo, um pedido de hipoteca e de cartão de crédito requer assinaturas legais de todos os mutuários e co-requerentes. Para habilitar fluxos de trabalho de assinatura eletrônica para cenários semelhantes, é possível integrar o Adobe Sign com o AEM Forms. Mais alguns exemplos são: você pode usar o Adobe Sign para:

* Feche negócios de qualquer dispositivo com processos de propostas, cotações e contratos totalmente automatizados.
* Conclua os processos de recursos humanos mais rapidamente e dê aos seus funcionários as experiências digitais.
* Reduza o tempo de ciclo de contratos e integre seus fornecedores mais rapidamente.
* Crie fluxos de trabalho digitais que automatizam processos comuns.

A integração do Adobe Sign com o AEM Forms suporta:

* Fluxos de trabalho de assinatura de usuário único e múltiplo
* Fluxos de trabalho de assinatura sequenciais e simultâneos
* Experiências de assinatura em forma e fora de forma
* Assinar formulários como um usuário anônimo ou conectado
* Processos de assinatura dinâmica (integração com o fluxo de trabalho do AEM Forms)
* Autenticação por meio de uma base de conhecimento, perfis de telefone e social

## Pré-requisitos {#prerequisites}

Antes de usar o Adobe Sign em um formulário adaptável:

* Verifique se o serviço em nuvem do AEM Forms está configurado para usar o Adobe Sign. Para obter detalhes, consulte [Integrar o Adobe Sign a formulários](../../forms/using/adobe-sign-integration-adaptive-forms.md)AEM.
* Mantenha a lista de signatários prontos. Você precisa de pelo menos um endereço de email para cada assinante.

## Configurar o Adobe Sign para um formulário adaptável {#configure-adobe-sign-for-an-adaptive-form}

Execute as seguintes etapas para configurar o Adobe Sign para um formulário adaptável:

1. [Editar propriedades de formulário adaptável para assinatura da Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Adicionar campos do Adobe Sign a um formulário adaptável](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Ativar o Adobe Sign para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Selecione o serviço Adobe Sign Cloud para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Adicionar assinantes do Adobe Sign a um formulário adaptável](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Selecione Enviar ação para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Detalhes do assinante](assets/signer_details_new.png)

### Editar propriedades de formulário adaptável para o Adobe Sign {#enableadobesign}

Configure as propriedades de formulário adaptável para o Adobe Sign para um formulário adaptável existente ou novo.

[Criar um formulário adaptável para o Adobe Sign](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) descreve as etapas para criar um formulário adaptável básico. Consulte [Criar um formulário](../../forms/using/creating-adaptive-form.md) adaptável para obter outras opções disponíveis ao criar um formulário adaptável.

#### Criar um formulário adaptável para o Adobe Sign {#create-an-adaptive-form-for-adobe-sign}

Execute as seguintes etapas para criar um formulário adaptável habilitado para assinatura:

1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulários]** > **[!UICONTROL Formulários e documentos]**.
1. Toque em **[!UICONTROL Criar]** e selecione Formulário **** adaptável. Uma lista de modelos é exibida. Selecione o modelo e toque em **[!UICONTROL Próximo]**.
1. Na guia **[!UICONTROL Básico]** :

   1. Especifique o **Nome** e o **Título** para o formulário adaptável.

   1. Selecione o contêiner [de](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) configuração criado ao configurar o Adobe Sign com formulários AEM.

1. Na guia Modelo **[!UICONTROL de]** formulário, selecione uma das seguintes opções:

   * Selecione o modelo de formulário **[!UICONTROL Associar como a opção de modelo]** Documento de registro e selecione um modelo Documento de registro. Se você usar um formulário adaptativo baseado em modelo de formulário, os documentos enviados para assinatura exibirão apenas os campos que se baseiam no modelo de formulário associado. Não exibe todos os campos do formulário adaptável.

   * Selecione a opção **[!UICONTROL Gerar documento de registro]** . Se você usar um formulário adaptável com a opção Documento de registro ativada, o documento enviado para assinatura exibirá todos os campos do formulário adaptável.

1. Toque em **[!UICONTROL Criar.]** É criado um formulário adaptável habilitado para assinatura, que pode ser usado para adicionar campos do Adobe Sign.

#### Editar um formulário adaptável para o Adobe Sign {#editafsign}

Execute as seguintes etapas para usar o Adobe Sign em um formulário adaptável existente:

1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulários]** > **[!UICONTROL Formulários e documentos]**.
1. Selecione o formulário adaptável e toque em **[!UICONTROL Propriedades]**.
1. Na guia **[!UICONTROL Básico]** , selecione o contêiner [de](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) configuração criado ao configurar o Adobe Sign com formulários AEM.
1. Na guia Modo **[!UICONTROL de]** formulário, selecione uma das seguintes opções:

   * Selecione o modelo de formulário **[!UICONTROL Associar como a opção de modelo]** Documento de registro e selecione um modelo Documento de registro. Se você usar um formulário adaptativo baseado em modelo de formulário, os documentos enviados para assinatura exibirão apenas os campos que se baseiam no modelo de formulário associado. Não exibe todos os campos do formulário adaptável.

   * Selecione a opção **[!UICONTROL Gerar documento de registro]** . Se você usar um formulário adaptável com a opção Documento de registro ativada, o documento enviado para assinatura exibirá todos os campos do formulário adaptável.

1. Toque em **[!UICONTROL Salvar e fechar]**. O formulário adaptável está habilitado para o Adobe Sign.

### Adicionar campos do Adobe Sign a um formulário adaptável {#addadobesignfieldstoanadaptiveform}

O Adobe Sign tem vários campos que podem ser colocados em um formulário adaptável. Esses campos aceitam vários tipos de dados, como assinaturas, iniciais, empresa ou título, e ajudam a coletar informações extras durante a assinatura, juntamente com as assinaturas. Você pode usar o componente Bloco de assinatura da Adobe para colocar os campos do Adobe Sign em vários locais em um formulário adaptável.

Execute as seguintes etapas para adicionar campos a um formulário adaptável e personalizar várias opções relacionadas a esses campos:

1. Arraste e solte o componente **Adobe Sign Block** do navegador de componentes para o formulário adaptável. O componente Bloco de assinatura da Adobe tem todos os campos do Adobe Sign suportados. Por padrão, adiciona um campo **Assinatura** ao formulário adaptável.

   ![Bloqueio de assinatura](assets/sign_block_new.png)

   Por padrão, o Bloco de assinatura da Adobe não fica visível no formulário adaptável publicado. Ela é visível somente nos documentos de assinatura. Você pode alterar a visibilidade do Bloco de assinatura da Adobe das propriedades do componente Bloco de assinatura da Adobe.

   >[!NOTE]
   >
   >    * O uso do bloco Adobe Sign não é obrigatório para usar o Adobe Sign em um formulário adaptável. Se você não usar o bloco do Adobe Sign e adicionar campos para os signatários, o campo de assinatura padrão será exibido na parte inferior dos documentos de assinatura.
   >    * Use o bloco Adobe Sign somente para os formulários adaptativos que geram automaticamente o Documento de registro. Se você estiver usando um XDP personalizado para gerar o Documento de registro ou um formulário adaptável baseado em modelo de formulário, o bloco Adobe Sign não será necessário.


1. Selecione o componente Bloco **do** Adobe Sign e toque no ícone **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png) . Exibe opções para adicionar campos e formatar a aparência de um campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **** A. Selecione e adicione campos do Adobe Sign. **** B. Expandir o bloco do Adobe Sign para a exibição em tela cheia

1. Toque no ícone **Adobe Sign Field** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) . Ele exibe opções para selecionar e adicionar campos do Adobe Sign.

   Expanda o campo **suspenso Tipo** para selecionar um campo Adobe Sign e toque no ícone ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) concluído para adicionar o campo selecionado ao bloco Adobe Sign. O campo suspenso **Tipo** inclui os tipos de campos Assinatura, Informações do assinante e Dados. Integração do Adobe Sign com os campos de suporte do AEM Forms listados somente na caixa suspensa Tipo. Para obter informações detalhadas sobre os campos do Adobe Sign, consulte a documentação [do](https://helpx.adobe.com/sign/help/field-types.html)Adobe Sign.

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   É obrigatório fornecer um nome exclusivo para um campo. Você também pode selecionar a opção necessária para marcar um campo como obrigatório. Além do **Nome** e da **** Opção obrigatória, alguns campos do Adobe Sign têm mais opções. Por exemplo, máscara e várias linhas. Além disso, especifique um nome exclusivo para cada campo do Adobe Sign se os campos residem no mesmo bloco do Adobe Sign ou em blocos diferentes.

   Se você selecionar Assinatura **** digital na lista suspensa, poderá aplicar assinaturas digitais ao formulário adaptável:

   * Online usando assinaturas em nuvem para assinar com uma ID [](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) digital hospedada por um provedor de serviços confiáveis.
   * Localmente, baixando o documento com o Adobe Acrobat ou Reader usando um cartão inteligente, um token USB ou uma ID digital baseada em arquivo.

### Ativar o Adobe Sign para um formulário adaptável {#enableadobsignforanadaptiveform}

A partir da caixa, o Adobe Sign não está ativado para um formulário adaptável. Execute as seguintes etapas para ativá-la:

1. No navegador de conteúdo, toque em Contêiner **de** formulário e toque no ícone **Configurar** ![configuração](assets/configure.png) . Ele abre o navegador de propriedades e exibe as propriedades do contêiner de Formulário adaptável.
1. No navegador de propriedades, expanda a opção Assinatura **** eletrônica e selecione a opção **Ativar o Adobe Sign** . Ela ativa o Adobe Sign para obter um formulário adaptável.

### Selecionar o serviço da Adobe Sign Cloud e a ordem de assinatura {#selectadobesigncloudserviceforanadaptiveform}

Você pode configurar vários serviços do Adobe Sign para uma instância do AEM Forms. É aconselhável ter um conjunto separado de serviços para cada função (Recursos Humanos, Finanças e muito mais). Facilita o rastreamento e a geração de relatórios de documentos assinados. Por exemplo, um banco tem vários departamentos. Você pode ter uma configuração separada para cada departamento para melhor rastreamento dos documentos.

Um documento também pode ter vários signatários. Por exemplo, uma solicitação de cartão de crédito pode ter vários candidatos. Um banco requer assinaturas de todos os candidatos antes de iniciar o processamento do pedido. Em cenários de vários signatários, você pode selecionar assinar o documento em ordem sequencial ou simultânea.

Execute as seguintes etapas para selecionar um serviço em nuvem e a ordem de assinatura:

![serviço em nuvem](assets/cloud-service.png)

1. No navegador de conteúdo, toque em Contêiner **de** formulário e toque no ícone **Configurar** ![configuração](assets/configure.png) . Ele abre o navegador de propriedades e exibe as propriedades do contêiner de Formulário adaptável.
1. No navegador de propriedades, expanda a opção Assinatura **** eletrônica e selecione a opção **Ativar o Adobe Sign** . Ela ativa o Adobe Sign para obter um formulário adaptável.
1. Selecione um serviço em nuvem na lista já configurada dos Adobe Sign Cloud Services.

   Se a lista **Adobe Sign Cloud Service** estiver vazia, siga o artigo [Configurar o Adobe Sign com formulários](../../forms/using/adobe-sign-integration-adaptive-forms.md) AEM para configurar o serviço.

1. Selecione a ordem de assinatura na caixa de diálogo **Os assinantes podem assinar** . Os cantores do Adobe Sign podem assinar um formulário adaptável **Sequencialmente** - um após outro assinante, ou **Simultaneamente** - em qualquer ordem.

   Em ordem sequencial, um assinante recebe o formulário para assinatura, de cada vez. Depois que um assinante concluir a assinatura do documento, o formulário será enviado para o próximo assinante e assim por diante.

   Em ordem simultânea, vários signatários podem assinar um formulário de cada vez.

1. [Adicione signatários a um formulário](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) adaptável e toque no ícone [aem_6_3_forms_save](assets/aem_6_3_forms_save.png) concluído para salvar as alterações.


### Adicionar signatários a um formulário adaptável {#addsignerstoanadaptiveform}

Você pode ter apenas um ou vários signatários para um formulário adaptável. Ao adicionar um assinante, você também pode configurar detalhes de autenticação para o assinante. Também é possível selecionar se o usuário e o cantor do formulário são a mesma pessoa. Execute as seguintes etapas para adicionar e fornecer vários detalhes sobre um assinante:

1. No navegador de conteúdo, toque em Contêiner **de** formulário e toque no ícone **Configurar** ![configuração](assets/configure.png) . Ele abre o navegador de propriedades com as propriedades do contêiner de Formulário adaptável.
1. No navegador de propriedades, expanda a opção Assinatura **** eletrônica e selecione a opção **Ativar o Adobe Sign** . Ela ativa o Adobe Sign para obter um formulário adaptável.
1. Toque em **Adicionar assinante** em Configuração **** do assinante. Ele adiciona um signatário ao formulário adaptativo. É possível adicionar vários signatários do Adobe Sign a um formulário adaptável.
1. ![detalhes telefônicos](assets/phone-details.png)

   Clique no ícone **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png) para especificar as seguintes informações sobre o assinante:

   * **** Título: Especifique um título para identificar exclusivamente um assinante.

   * **** O assinante e a pessoa que preenche o formulário são os mesmos?: Selecione **Sim** se o usuário e o primeiro assinante forem a mesma pessoa. Se a opção estiver definida como **Não,** não use o componente de etapa de assinatura no formulário adaptável. Se o formulário contiver um componente Etapa de assinatura, o campo será automaticamente definido como Sim.

   * **** Endereço de email do assinante: Especifique o endereço de email do assinante. O assinante recebe para ser assinado em documentos/formulário no endereço de email especificado. Você pode optar por usar um endereço de email fornecido em um campo de formulário, no perfil de usuário do AEM do usuário conectado ou inserir manualmente um endereço de email. Trata-se de um passo obrigatório. Verifique se o endereço de email do primeiro assinante ou do único assinante (no caso de um único assinante) não é idêntico à conta do Adobe Sign usada para configurar os serviços em nuvem do AEM.

   * **** Método de autenticação do assinante: Especifique o método para autenticar um usuário antes de abrir um formulário para assinatura. Você pode escolher entre autenticação por telefone, base de conhecimento e baseada em identidade social.
   >[!NOTE]
   >
   >    * Por padrão, a autenticação baseada em identidade social fornece uma opção para autenticação usando Facebook, Google e LinkedIn. Você pode entrar em contato com o suporte do Adobe Sign para ativar outros provedores de autenticação social.


   * **** Campos do Adobe Sign para preencher ou assinar: Selecione os campos do Adobe Sign para o assinante. Um formulário adaptável pode ter vários campos do Adobe Sign. Você pode optar por ativar campos específicos para um assinante. O campo exibe todos os Blocos de assinatura da Adobe disponíveis. Quando você seleciona um bloco, todos os campos do bloco são selecionados. Você pode usar o ícone X para desmarcar um campo.
   ![detalhes do assinante](assets/signer-details.png)

   A imagem acima tem dois exemplos de blocos de assinatura da Adobe: Informações pessoais e detalhes do escritório

   Toque no ícone ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) concluído. O assinante é adicionado e configurado.

### Selecione Enviar ação para um formulário adaptável {#selectsubmitactionforanadaptiveform}

Depois que você adicionar campos do Adobe Sign a um formulário adaptável, ativar o Adobe Sign no contêiner de formulário, selecionar Adobe Sign Cloud Service e adicionar assinantes do Adobe Sign, selecione uma ação de envio apropriada para o formulário adaptável. Para obter informações detalhadas sobre ações de envio de formulários adaptáveis, consulte [Configuração da ação](../../forms/using/configuring-submit-actions.md)Enviar.

Além disso, um formulário adaptativo habilitado para o Adobe Sign é enviado somente depois que todos os signatários assinam o formulário. Você pode encontrar um formulário parcialmente assinado na seção Assinatura pendente do portal de formulários. O Adobe Sign Configuration Service continua pesquisando o servidor Adobe Sign em intervalos [](../../forms/using/adobe-sign-integration-adaptive-forms.md) regulares para verificar o status das assinaturas. Se todos os signatários concluírem a assinatura do formulário, o serviço de ação de envio será iniciado e o formulário será enviado. Se você estiver usando uma ação de envio personalizada e o formulário usar o Adobe Sign, atualize sua ação de envio personalizada para usar o serviço de ação de envio.

>[!NOTE]
>
>Os dados do formulário adaptável são armazenados temporariamente no Portal do Forms. É recomendável usar armazenamento [personalizado para o Portal](/help/forms/using/configuring-draft-submission-storage.md)do Forms. Ela garante que os dados de PII (informações de identificação pessoal) não sejam armazenados em servidores AEM.

Sua experiência de assinatura de formulário está pronta. É possível visualizar o formulário para verificar a experiência de assinatura. No formulário publicado, os campos Adobe Sign Block são exibidos quando um assinante recebe o formulário para assinatura por meio de um email. Essa experiência também é conhecida como experiência de assinatura fora de forma. Você também pode configurar uma experiência de assinatura no formulário para o primeiro assinante, para obter etapas detalhadas, consulte [Criar experiência](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)de assinatura no formulário.

## Configurar assinaturas em nuvem para um formulário adaptável {#configure-cloud-signatures-for-an-adaptive-form}

Assinaturas digitais ou remotas baseadas em nuvem são uma nova geração de assinaturas digitais que funcionam em computadores, dispositivos móveis e na Web. e atender aos mais altos níveis de conformidade e garantia para autenticação de assinante. Você pode assinar um formulário adaptável com assinaturas digitais baseadas em nuvem.

Depois de [editar as propriedades do formulário adaptável para o Adobe sign](../../forms/using/working-with-adobe-sign.md#enableadobesign), execute as seguintes etapas para adicionar o campo de assinatura na nuvem a um formulário adaptável:

1. Arraste e solte o componente **Adobe Sign Block** do navegador de componentes para o formulário adaptável. O componente Bloco de assinatura da Adobe tem todos os campos do Adobe Sign suportados. Por padrão, adiciona um campo **Assinatura** ao formulário adaptável.

   ![Bloqueio de assinatura](assets/sign-block-new.png)

1. Selecione o componente Bloco **do** Adobe Sign e toque no ícone **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png) . Exibe opções para adicionar campos e formatar a aparência de um campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **** A. Selecione e adicione campos do Adobe Sign. **** B. Expandir o bloco do Adobe Sign para a exibição em tela cheia

1. Toque no ícone **Adobe Sign Field** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) . Ele exibe opções para selecionar e adicionar campos do Adobe Sign.

   Expanda o campo **suspenso Tipo** para selecionar Assinatura **** digital e toque no ícone Concluído para adicionar o campo selecionado ao bloco Adobe Sign.

   ![Assinaturas digitais](assets/digital_signatures_new.png)

   É obrigatório fornecer um nome exclusivo para um campo.

   Aplique assinaturas digitais ao formulário adaptável usando:

   * Assinaturas da nuvem: Faça logon com uma ID [](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) digital hospedada por um provedor de serviços de confiança.
   * Adobe Acrobat ou Reader: Baixe e abra o documento com o Adobe Acrobat ou Reader para fazer logon usando um cartão inteligente, um token USB ou uma ID digital baseada em arquivo.
   Após adicionar o campo de assinatura na nuvem ao formulário adaptável, execute as seguintes etapas para concluir o processo de configuração:

   * [Ativar o Adobe Sign para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Selecione o serviço Adobe Sign Cloud para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Adicionar assinantes do Adobe Sign a um formulário adaptável](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Selecione Enviar ação para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## Criar experiência de assinatura no formulário {#create-in-form-signing-experience}

Um usuário também pode assinar um formulário adaptável enquanto preenche o formulário. Essa experiência também é conhecida como experiência de assinatura no formulário. A experiência de assinatura no formulário está disponível somente para o primeiro cantor em um ambiente com vários signatários. Execute as seguintes etapas para criar uma experiência de assinatura no formulário para um formulário adaptável:

1. [Adicione e configure o componente](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)Etapa de assinatura.
1. [Adicione o componente](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component)Etapa de resumo.

![Experiência de assinatura no formulário](assets/in_form_signing_experience_new.png)

### Adicionar e configurar o componente Etapa de assinatura {#add-and-configure-the-signature-step-component}

Use o componente Etapa de assinatura para fornecer uma área para assinar eletronicamente o formulário preenchido. Quando a seção que contém o componente Etapa de assinatura é renderizada, exibe uma versão PDF assinável do formulário preenchido. O componente Etapa de assinatura ocupa a largura total disponível para o formulário. É recomendável não ter nenhum outro componente na seção que contém o componente Etapa de assinatura.

Execute as seguintes etapas para configurar o componente Etapa de assinatura:

1. Arraste e solte o componente Etapa **da** assinatura do navegador Componentes para o formulário.
1. Selecione o componente recém-adicionado da etapa Assinatura e toque no ícone **Configurar** ![configuração](assets/configure.png) . Ele abre o navegador de propriedades e exibe as propriedades da etapa de assinatura. Configure as seguintes propriedades:

   * **Nome** do elemento: Especifique o nome do componente.

   * **** Título: Especifique o título exclusivo do componente.
   * **** Mensagem do modelo: Especifique a mensagem a ser exibida enquanto o PDF de assinatura estiver sendo carregado. Os serviços Adobe Sign levam algum tempo para preparar e carregar um PDF de assinatura.
   * **** Serviço de assinatura: Selecione a opção **Adobe Sign** .

   * **Usar componente** herdado de assinatura eletrônica: Se você estiver usando o respectivo formulário adaptável no [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), no aplicativo AEM Forms ou se o formulário adaptativo subjacente tiver um componente de e-sign herdado, selecione a opção **Usar componente** de E-sign herdado.

   * **Configuração**: Selecione uma configuração (Adobe Sign Cloud Service). A caixa suspensa estará disponível somente se a opção **Usar componente** de assinatura eletrônica herdado estiver ativada.
   Toque no ícone ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) concluído para salvar as alterações.

   ![Etapa de assinatura](assets/signature_step_new.png)

   >[!NOTE]
   >
   >    * Ao arrastar e soltar o componente Etapa **[!UICONTROL de]** assinatura no formulário, o signatário **[!UICONTROL é o mesmo e a pessoa que preenche o formulário?]** é automaticamente definida como **Sim**. É necessário manter o formulário funcionando.
      >
      >    
   * Os formulários adaptativos ativados do Adobe Sign não são compatíveis com o uso do botão Enviar na seção ou no painel usando o componente Etapa de assinatura. Você pode adicionar uma etapa de resumo após a etapa Assinatura para o envio manual ou uma submissão automática é acionada após o intervalo definido usando o Serviço [de configuração do](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status)Adobe Sign.


### Configurar a página de agradecimento ou o componente de etapa de resumo {#configure-the-thank-you-page-or-summary-step-component}

O componente Etapa **de** resumo envia automaticamente o formulário, preenche as informações na página Resumo personalizada e exibe o resumo do formulário enviado. Ele também obtém as informações necessárias no mapa de retorno. O componente Etapa de resumo ocupa a largura total disponível para o formulário. É recomendável não ter nenhum outro componente na seção que contenha o componente de Etapa de resumo.

Agora, a experiência de assinatura no formulário está pronta. É possível visualizar o formulário para verificar a experiência de assinatura.

## Frequently asked questions {#frequently-asked-questions}

**** Ans: Não, o AEM Forms não é compatível com o uso de um formulário adaptável que incorpora um formulário adaptativo habilitado para assinatura do Adobe Sign

**** Ans: O formulário adaptável criado usando o modelo avançado está configurado para usar o Adobe Sign. Para resolver o erro, crie e selecione uma configuração de nuvem do Adobe Sign e configure um assinante do Adobe Sign para o formulário adaptável.

**** Ans: Sim, você pode usar tags de texto em um componente de texto para adicionar campos do Adobe Sign a um formulário adaptável habilitado para [Documento de registro](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) (Somente para documento gerado automaticamente da opção de registro). Para saber mais sobre o procedimento e as regras para criar uma tag de texto, consulte Documentação [do](https://helpx.adobe.com/sign/help/text-tags.html)Adobe Sign. Observe também que os formulários adaptativos têm suporte limitado para tags de texto. Você pode usar as tags de texto para criar apenas os campos compatíveis com o [Adobe Sign Block](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) .

**** Ans: É possível usar ambos os componentes simultaneamente em um formulário. Estas são algumas recomendações para o uso desses componentes:

**** Bloco do Adobe Sign: Você pode usar o Bloco de assinatura da Adobe para adicionar campos do Adobe Sign em qualquer lugar no formulário adaptável. Também ajuda a atribuir campos específicos a signatários. Por padrão, quando um formulário adaptável é visualizado ou publicado, o Adobe Sign Block não fica visível. Esses blocos são ativados somente no documento de assinatura. No documento de assinatura, somente os campos atribuídos a um assinante são ativados. O bloco do Adobe Sign pode ser usado com o primeiro e os signatários subsequentes.

**** Componente da etapa de assinatura: Você pode usar o componente de etapa de assinatura para criar uma experiência de assinatura no formulário. Ela permite que somente o primeiro assinante assine enquanto o formulário está sendo preenchido. Quando a seção que contém o componente Etapa de assinatura é renderizada, exibe uma versão PDF assinável do formulário. Geralmente, é a última ou penúltima seção seguida do componente de resumo de um formulário.

## Solução de problemas {#troubleshoot}

### Falhas no contrato do Adobe Sign {#adobe-sign-agreement-failures}

**Problema** Quando o serviço Adobe Sign é configurado para um formulário adaptável, o serviço falha ao criar um contrato Adobe Sign para o formulário adaptativo subjacente.

**Resolução**

* Verifique a [configuração do serviço](../../forms/using/adobe-sign-integration-adaptive-forms.md) de nuvem do Adobe Sign usado no formulário adaptável.
* Certifique-se de que o aplicativo da API no servidor Adobe Sign usado para configurar o serviço Adobe Sign Cloud tenha as permissões necessárias.
* Se você estiver usando vários serviços da Adobe Sign Cloud, aponte o URL **[!UICONTROL de autenticação]** de todos os serviços para o mesmo **[!UICONTROL Adobe Sign Shard]**.

* Use endereços de email separados para configurar a conta do Adobe Sign e para o primeiro assinante e único assinante. O endereço de email do primeiro assinante ou do único assinante (no caso do assinante único) não pode ser idêntico à conta do Adobe Sign usada para configurar os serviços em nuvem do AEM.

## Artigos relacionados {#related-articles}

* [Integrar o Adobe Sign ao AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Usar o Adobe Sign em um formulário adaptável](../../forms/using/working-with-adobe-sign.md)

* [Usar o Adobe Sign com formulários AEM (Vídeo)
   ](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
