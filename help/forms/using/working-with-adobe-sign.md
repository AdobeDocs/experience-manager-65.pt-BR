---
title: Uso do Adobe Sign em um formulário adaptável
seo-title: Uso do Adobe Sign em um formulário adaptável
description: Ative workflows de assinatura eletrônica (Adobe Sign) para um formulário adaptável para automatizar workflows de assinatura, simplificar processos de assinatura única e múltipla e assinar eletronicamente formulários de dispositivos móveis.
seo-description: Ative workflows de assinatura eletrônica (Adobe Sign) para um formulário adaptável para automatizar workflows de assinatura, simplificar processos de assinatura única e múltipla e assinar eletronicamente formulários de dispositivos móveis.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
translation-type: tm+mt
source-git-commit: 70fff9b4029ba70fe0667dafa69fc6172f4b1733
workflow-type: tm+mt
source-wordcount: '3755'
ht-degree: 0%

---


# Usar [!DNL Adobe Sign] em um formulário adaptável{#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] habilita workflows de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os workflows para processar documentos para áreas legais, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e outras.

Em um cenário típico de [!DNL Adobe Sign] e formulários adaptativos, um usuário preenche um formulário adaptável para se candidatar a um serviço. Por exemplo, um pedido de hipoteca e de cartão de crédito requer assinaturas legais de todos os mutuários e co-requerentes. Para ativar workflows de assinatura eletrônica para cenários semelhantes, é possível integrar [!DNL Adobe Sign] com AEM [!DNL Forms]. Mais alguns exemplos são: você pode usar [!DNL Adobe Sign] para:

* Feche negócios de qualquer dispositivo com processos de propostas, cotações e contratos totalmente automatizados.
* Conclua os processos de recursos humanos mais rapidamente e dê aos seus funcionários as experiências digitais.
* Reduza o tempo de ciclo de contratos e integre seus fornecedores mais rapidamente.
* Crie workflows digitais que automatizam processos comuns.

[!DNL Adobe Sign] a integração com AEM  [!DNL Forms] suporta:

* Workflows de assinatura de usuário único e múltiplo
* Workflows de assinatura sequenciais e simultâneos
* Experiências de assinatura em forma e fora de forma
* Assinar formulários como um usuário anônimo ou conectado
* Processos de assinatura dinâmica (integração com AEM [!DNL Forms] fluxo de trabalho)
* Autenticação por meio de uma base de conhecimento, telefone e perfis sociais

## Pré-requisitos {#prerequisites}

Antes de usar [!DNL Adobe Sign] em um formulário adaptável:

* Verifique se o serviço de nuvem AEM [!DNL Forms] está configurado para usar [!DNL Adobe Sign]. Para obter detalhes, consulte [Integrar o Adobe Sign ao AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* Mantenha a lista dos signatários prontos. Você precisa de pelo menos um endereço de email para cada assinante.

## Configure [!DNL Adobe Sign] para um formulário adaptável {#configure-adobe-sign-for-an-adaptive-form}

Execute as seguintes etapas para configurar [!DNL Adobe Sign] para um formulário adaptável:

1. [Editar propriedades de formulário adaptável para sinal de Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Adicionar campos do Adobe Sign a um formulário adaptável](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Habilitar Adobe Sign para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Selecione o Cloud Service Adobe Sign para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Adicionar signatários do Adobe Sign a um formulário adaptável](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Selecione Enviar ação para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Detalhes do assinante](assets/signer_details_new.png)

### Editar propriedades de formulário adaptável para [!DNL Adobe Sign] {#enableadobesign}

Configure as propriedades de formulário adaptável para [!DNL Adobe Sign] para um formulário existente ou novo.

[Crie um formulário adaptável para Adobe ](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) Signature descreve as etapas para criar um formulário adaptável básico. Consulte [Criar um formulário adaptável](../../forms/using/creating-adaptive-form.md) para obter outras opções disponíveis ao criar um formulário adaptável.

#### Criar um formulário adaptável para [!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}

Execute as seguintes etapas para criar um formulário adaptável habilitado para assinatura:

1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documentos]**.
1. Toque em **[!UICONTROL Criar]** e selecione **[!UICONTROL Formulário adaptável]**. Uma lista de modelos é exibida. Selecione o modelo e toque em **[!UICONTROL Next]**.
1. Na guia **[!UICONTROL Basic]**:

   1. Especifique **[!UICONTROL Name]** e **[!UICONTROL Title]** para o formulário adaptável.

   1. Selecione o container de configuração [criado ao configurar [!DNL Adobe Sign] com AEM [!DNL Forms].](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)

      >[!NOTE]
      >
      >A lista suspensa **[!UICONTROL Adobe Sign Cloud Service]** exibe os serviços em nuvem configurados no container de configuração selecionado neste campo. A lista suspensa **[!UICONTROL Adobe Sign Cloud Service]** está disponível na seção **[!UICONTROL Assinatura Eletrônica]** das propriedades de formulário adaptável quando você seleciona a opção **[!UICONTROL Ativar Adobe Sign]**.

1. Na guia **[!UICONTROL Modelo de formulário]**, selecione uma das seguintes opções:

   * Selecione a opção **[!UICONTROL Associar modelo de formulário como o Documento do modelo de Registro]** e selecione um Documento de modelo de Registro. Se você usar um formulário adaptativo baseado em modelo de formulário, os documentos enviados para assinatura exibirão apenas os campos que se baseiam no modelo de formulário associado. Não exibe todos os campos do formulário adaptável.

   * Selecione a opção **[!UICONTROL Gerar Documento de Record]**. Se você usar um formulário adaptável habilitado para a opção Documento de registro, o documento enviado para assinatura exibirá todos os campos do formulário adaptável.

1. Toque em **[!UICONTROL Criar.]** É criado um formulário adaptativo habilitado para assinatura, que pode ser usado para adicionar  [!DNL Adobe Sign] campos.

#### Editar um formulário adaptável para [!DNL Adobe Sign] {#editafsign}

Execute as seguintes etapas para usar [!DNL Adobe Sign] em um formulário adaptável existente:

1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documentos]**.
1. Selecione o formulário adaptável e toque em **[!UICONTROL Propriedades]**.
1. Na guia **[!UICONTROL Basic]**, selecione o [container de configuração](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) criado ao configurar [!DNL Adobe Sign] com AEM [!DNL Forms].
1. Na guia **[!UICONTROL Modelo de formulário]**, selecione uma das seguintes opções:

   * Selecione a opção **[!UICONTROL Associar modelo de formulário como o Documento do modelo de Registro]** e selecione um Documento de modelo de Registro. Se você usar um formulário adaptativo baseado em modelo de formulário, os documentos enviados para assinatura exibirão apenas os campos que se baseiam no modelo de formulário associado. Não exibe todos os campos do formulário adaptável.

   * Selecione a opção **[!UICONTROL Gerar Documento de Record]**. Se você usar um formulário adaptável habilitado para a opção Documento de registro, o documento enviado para assinatura exibirá todos os campos do formulário adaptável.

1. Toque em **[!UICONTROL Salvar e fechar]**. O formulário adaptável está ativado para [!DNL Adobe Sign].

### Adicionar campos Adobe Sign a um formulário adaptável {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] tem vários campos que podem ser colocados em um formulário adaptável. Esses campos aceitam vários tipos de dados, como assinaturas, iniciais, empresa ou título, e ajudam a coletar informações extras durante a assinatura, juntamente com as assinaturas. Você pode usar o componente [!DNL Adobe Sign] Bloquear para colocar os campos [!DNL Adobe Sign] em vários locais em um formulário adaptável.

Execute as seguintes etapas para adicionar campos a um formulário adaptável e personalizar várias opções relacionadas a esses campos:

1. Arraste e solte o componente **[!UICONTROL Adobe Sign Block]** do navegador de componentes para o formulário adaptável. O componente [!DNL Adobe Sign] Block tem todos os campos [!DNL Adobe Sign] suportados. Por padrão, adiciona um campo **Signature** ao formulário adaptável.

   ![Bloqueio de assinatura](assets/sign_block_new.png)

   Por padrão, o bloco [!DNL Adobe Sign] não está visível no formulário adaptável publicado. Ela é visível somente nos documentos de assinatura. Você pode alterar a visibilidade de [!DNL Adobe Sign] Bloco a partir das propriedades do componente [!DNL Adobe Sign] Bloco.

   >[!NOTE]
   >
   >    * O uso do bloco [!DNL Adobe Sign] não é obrigatório para usar [!DNL Adobe Sign] em um formulário adaptável. Se você não usar [!DNL Adobe Sign] bloquear e adicionar campos para os signatários, o campo de assinatura padrão será exibido na parte inferior dos documentos de assinatura.
   >    * Use o bloco [!DNL Adobe Sign] somente para os formulários adaptáveis que geram automaticamente o Documento de Registro. Se você estiver usando um XDP personalizado para gerar Documento de Registro ou um formulário adaptável baseado em modelo de formulário, o bloco [!DNL Adobe Sign] não será necessário.


1. Selecione o componente **[!UICONTROL Adobe Sign Block]** e toque no ícone **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png). Exibe opções para adicionar campos e formatar a aparência de um campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Selecione e adicione  [!DNL Adobe Sign] campos. **B.** Expanda o  [!DNL Adobe Sign] bloco para a visualização de tela cheia

1. Toque no ícone **[!UICONTROL Adobe Sign] Field** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png). Ele exibe opções para selecionar e adicionar campos [!DNL Adobe Sign].

   Expanda o campo suspenso **[!UICONTROL Tipo]** para selecionar um campo [!DNL Adobe Sign] e toque no ícone Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para adicionar o campo selecionado ao bloco [!DNL Adobe Sign]. O campo suspenso **[!UICONTROL Tipo]** inclui os tipos de campos Assinatura, Informações do assinante e Dados. [!DNL Adobe Sign] integração com AEM campos de  [!DNL Forms] suporte listados somente na caixa   suspensa Tipo. Para obter informações detalhadas sobre os campos [!DNL Adobe Sign], consulte [documentação da Adobe Sign](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   É obrigatório fornecer um nome exclusivo para um campo. Você também pode selecionar a opção necessária para marcar um campo como obrigatório. Além da opção **[!UICONTROL Name]** e **[!UICONTROL Required]**, alguns campos [!DNL Adobe Sign] têm mais opções. Por exemplo, máscara e várias linhas. Além disso, especifique um nome exclusivo para cada campo [!DNL Adobe Sign] se os campos residem no mesmo bloco ou em blocos [!DNL Adobe Sign] diferentes.

   Se você selecionar **[!UICONTROL Assinatura digital]** na lista suspensa, poderá aplicar assinaturas digitais ao formulário adaptável:

   * Online usando assinaturas em nuvem para assinar com uma [ID digital](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) hospedada por um provedor de serviço de confiança.
   * Localmente, baixando o documento com Adobe Acrobat ou Reader usando um cartão inteligente, um token USB ou uma ID digital baseada em arquivo.

### Ative [!DNL Adobe Sign] para um formulário adaptável {#enableadobsignforanadaptiveform}

A partir da caixa, [!DNL Adobe Sign] não está ativado para um formulário adaptável. Execute as seguintes etapas para ativá-la:

1. No navegador de conteúdo, toque em **[!UICONTROL Container de formulário]** e toque no ícone **[!UICONTROL Configurar]** ![configurar](assets/configure.png). Ele abre o navegador de propriedades e exibe as propriedades do container de formulário adaptável.
1. No navegador de propriedades, expanda a opção **[!UICONTROL Assinatura eletrônica]** e selecione a opção **[!UICONTROL Habilitar Adobe Sign]**. Ela ativa [!DNL Adobe Sign] para um formulário adaptável.

### Selecionar [!DNL Adobe Sign] Cloud Service e ordem de assinatura {#selectadobesigncloudserviceforanadaptiveform}

Você pode configurar vários serviços [!DNL Adobe Sign] para uma instância de AEM [!DNL Forms]. É aconselhável ter um conjunto separado de serviços para cada função (Recursos humanos, finanças e muito mais). Facilita o rastreamento e o relatórios de documentos assinados. Por exemplo, um banco tem vários departamentos. Você pode ter uma configuração separada para cada departamento para melhor rastreamento dos documentos.

Um documento também pode ter vários signatários. Por exemplo, uma solicitação de cartão de crédito pode ter vários candidatos. Um banco requer assinaturas de todos os candidatos antes de iniciar o processamento do pedido. Para cenários com vários signatários, você pode optar por assinar o documento em ordem sequencial ou simultânea.

Execute as seguintes etapas para selecionar um serviço em nuvem e a ordem de assinatura:

![serviço em nuvem](assets/cloud-service.png)

1. No navegador de conteúdo, toque em **[!UICONTROL Container de formulário]** e toque no ícone **[!UICONTROL Configurar]** ![configurar](assets/configure.png). Ele abre o navegador de propriedades e exibe as propriedades do container de formulário adaptável.
1. No navegador de propriedades, expanda a opção **[!UICONTROL Assinatura eletrônica]** e selecione a opção **[!UICONTROL Habilitar Adobe Sign]**. Ela ativa [!DNL Adobe Sign] para um formulário adaptável.
1. Selecione um serviço em nuvem na lista já configurada de [!DNL Adobe Sign] Cloud Services.

   Se a lista **[!UICONTROL Adobe Sign Cloud Service]** estiver vazia, siga o artigo [Configurar o Adobe Sign com o AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) para configurar o serviço.

   A lista suspensa lista os serviços em nuvem existentes na pasta `global` em Ferramentas > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Além disso, o menu suspenso também lista os serviços em nuvem existentes na pasta selecionada no campo **[!UICONTROL Container de configuração]** ao criar um formulário adaptável.

1. Selecione a ordem de assinatura na caixa de diálogo **[!UICONTROL Os assinantes podem assinar]**. [!DNL Adobe Sign] os cantores podem assinar um formulário adaptável  **[!UICONTROL Sequencialmente]**  - um após o outro assinante, ou  **[!UICONTROL Simultaneamente]**  - em qualquer ordem.

   Em ordem sequencial, um assinante recebe o formulário para assinatura, de cada vez. Depois que um assinante concluir a assinatura do documento, o formulário será enviado para o próximo assinante e assim por diante.

   Em ordem simultânea, vários signatários podem assinar um formulário de cada vez.

1. [Adicione signatários a um ](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) formato adaptável e toque no ícone  ![aem_6_3_forms_](assets/aem_6_3_forms_save.png) saveicon concluído para salvar as alterações.


### Adicionar signatários a um formulário adaptável {#addsignerstoanadaptiveform}

Você pode ter apenas um ou vários signatários para um formulário adaptável. Ao adicionar um assinante, você também pode configurar detalhes de autenticação para o assinante. Também é possível selecionar se o usuário e o cantor do formulário são a mesma pessoa. Execute as seguintes etapas para adicionar e fornecer vários detalhes sobre um assinante:

1. No navegador de conteúdo, toque em **[!UICONTROL Container de formulário]** e toque no ícone **[!UICONTROL Configurar]** ![configurar](assets/configure.png). Ele abre o navegador de propriedades com as propriedades do container de formulário adaptável.
1. No navegador de propriedades, expanda a opção **[!UICONTROL Assinatura eletrônica]** e selecione a opção **[!UICONTROL Habilitar Adobe Sign]**. Ela ativa [!DNL Adobe Sign] para um formulário adaptável.
1. Toque em **[!UICONTROL Adicionar assinante]** em **[!UICONTROL Configuração do assinante]**. Ele adiciona um signatário ao formulário adaptativo. É possível adicionar vários signatários [!DNL Adobe Sign] a um formulário adaptável.
   ![detalhes telefônicos](assets/phone-details.png)

1. Clique no ícone **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png) para especificar as seguintes informações sobre o assinante:

   * **[!UICONTROL Título]:** especifique um título para identificar exclusivamente um assinante.

   * **[!UICONTROL A pessoa que assina e que preenche o formulário são a mesma pessoa?]:** Selecione  **Sim** se o usuário e o primeiro assinante forem a mesma pessoa. Se a opção estiver definida como **Não,**, não use o componente de etapa de assinatura no formulário adaptável. Se o formulário contiver um componente Etapa de assinatura, o campo será automaticamente definido como Sim.

   * **[!UICONTROL Endereço] de email do assinante:** especifique o endereço de email do assinante. O assinante recebe para ser assinado documentos/formulário no endereço de email especificado. Você pode optar por usar um endereço de email fornecido em um campo de formulário, AEM perfil do usuário conectado ou inserir manualmente um endereço de email. Trata-se de um passo obrigatório. Verifique se o endereço de email do primeiro assinante ou do único assinante (no caso de um único assinante) não é idêntico à conta [!DNL Adobe Sign] usada para configurar os serviços em nuvem do AEM.

   * **[!UICONTROL Método] de autenticação do assinante:** especifique o método para autenticar um usuário antes de abrir um formulário para assinatura. Você pode escolher entre autenticação por telefone, base de conhecimento e baseada em identidade social.
   >[!NOTE]
   >
   >    * Por padrão, a autenticação baseada em identidade social fornece uma opção para autenticação usando o Facebook, o Google e o LinkedIn. Você pode entrar em contato com o suporte [!DNL Adobe Sign] para ativar outros provedores de autenticação social.


   * **[!DNL Adobe Sign]campos para preencher ou assinar:** Selecione  [!DNL Adobe Sign] campos para o assinante. Um formulário adaptável pode ter vários campos [!DNL Adobe Sign]. Você pode optar por ativar campos específicos para um assinante. O campo exibe todos os [!DNL Adobe Sign] Blocos disponíveis. Quando você seleciona um bloco, todos os campos do bloco são selecionados. Você pode usar o ícone X para desmarcar um campo.

   ![detalhes do assinante](assets/signer-details.png)

   A imagem acima tem dois exemplos de [!DNL Adobe Sign] blocos: Informações pessoais e detalhes do escritório

   Toque no ícone Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). O assinante é adicionado e configurado.

### Selecione Enviar ação para um formulário adaptável {#selectsubmitactionforanadaptiveform}

Depois de adicionar os campos [!DNL Adobe Sign] a um formulário adaptável, habilitar [!DNL Adobe Sign] a partir do container do formulário, selecionar [!DNL Adobe Sign] Cloud Service e adicionar [!DNL Adobe Sign] signatários, selecione uma ação de envio apropriada para o formulário adaptativo. Para obter informações detalhadas sobre ações de envio de formulários adaptáveis, consulte [Configuração da ação Enviar](../../forms/using/configuring-submit-actions.md).

Além disso, um formulário adaptativo habilitado para [!DNL Adobe Sign] é enviado somente depois que todos os signatários assinam o formulário. Você pode encontrar um formulário parcialmente assinado na seção Assinatura pendente do portal de formulários. [!DNL Adobe Sign] O Serviço de Configuração mantém o  [!DNL Adobe Sign] servidor de pesquisa em  [intervalos regulares ](../../forms/using/adobe-sign-integration-adaptive-forms.md) para verificar o status das assinaturas. Se todos os signatários concluírem a assinatura do formulário, o serviço de ação de envio será iniciado e o formulário será enviado. Se você estiver usando uma ação de envio personalizada e o formulário usar [!DNL Adobe Sign], atualize sua ação de envio personalizada para usar o serviço de ação de envio.

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

Sua experiência de assinatura de formulário está pronta. Você pode pré-visualização o formulário para verificar a experiência de assinatura. No formulário publicado, os campos [!DNL Adobe Sign] Bloquear são exibidos quando um assinante recebe o formulário para assinatura por meio de um email. Essa experiência também é conhecida como experiência de assinatura fora de forma. Você também pode configurar uma experiência de assinatura no formulário para o primeiro assinante, para obter etapas detalhadas, consulte [Criar experiência de assinatura no formulário](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## Configurar assinaturas em nuvem para um formulário adaptável {#configure-cloud-signatures-for-an-adaptive-form}

Assinaturas digitais ou remotas baseadas em nuvem são uma nova geração de assinaturas digitais que funcionam em computadores, dispositivos móveis e na Web. e atender aos mais altos níveis de conformidade e garantia para autenticação de assinante. Você pode assinar um formulário adaptável com assinaturas digitais baseadas em nuvem.

Depois de [editar as propriedades do formulário adaptável para o sinal de Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign), execute as seguintes etapas para adicionar o campo de assinatura na nuvem a um formulário adaptável:

1. Arraste e solte o componente **[!UICONTROL Adobe Sign Block]** do navegador de componentes para o formulário adaptável. O componente [!UICONTROL Adobe Sign Block] tem todos os campos [!DNL Adobe Sign] suportados. Por padrão, adiciona um campo **[!UICONTROL Signature]** ao formulário adaptável.

   ![Bloqueio de assinatura](assets/sign-block-new.png)

1. Selecione o componente **[!UICONTROL Adobe Sign Block]** e toque no ícone **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png). Exibe opções para adicionar campos e formatar a aparência de um campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Selecione e adicione  [!DNL Adobe Sign] campos. **B.** Expanda o  [!DNL Adobe Sign] bloco para a visualização de tela cheia

1. Toque no ícone **[!UICONTROL Campo do Adobe Sign]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png). Ele exibe opções para selecionar e adicionar campos [!DNL Adobe Sign].

   Expanda o campo suspenso **[!UICONTROL Type]** para selecionar **[!UICONTROL Assinatura Digital]** e toque no ícone **Done** para adicionar o campo selecionado ao bloco [!DNL Adobe Sign].

   ![Assinaturas digitais](assets/digital_signatures_new.png)

   É obrigatório fornecer um nome exclusivo para um campo.

   Aplique assinaturas digitais ao formulário adaptável usando:

   * Assinaturas da nuvem: Assine com uma [ID digital](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) hospedada por um provedor de serviço de confiança.
   * Adobe Acrobat ou Reader: Baixe e abra o documento com Adobe Acrobat ou Reader para assinar usando um cartão inteligente, um token USB ou uma ID digital baseada em arquivo.

   Depois de adicionar o campo de assinatura na nuvem ao formulário adaptável, execute as seguintes etapas para concluir o processo de configuração:

   * [Habilitar Adobe Sign para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Selecione o Cloud Service Adobe Sign para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Adicionar signatários do Adobe Sign a um formulário adaptável](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Selecione Enviar ação para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## Criar experiência de assinatura no formulário {#create-in-form-signing-experience}

Um usuário também pode assinar um formulário adaptável enquanto preenche o formulário. Essa experiência também é conhecida como experiência de assinatura no formulário. A experiência de assinatura no formulário está disponível somente para o primeiro cantor em um ambiente com vários signatários. Execute as seguintes etapas para criar uma experiência de assinatura no formulário para um formulário adaptável:

1. [Adicione e configure o componente](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component) Etapa de assinatura.
1. [Adicione o componente](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component) Etapa de resumo.

![Experiência de assinatura no formulário](assets/in_form_signing_experience_new.png)

### Adicionar e configurar o componente Etapa de assinatura {#add-and-configure-the-signature-step-component}

Use o componente Etapa de assinatura para fornecer uma área para assinar eletronicamente o formulário preenchido. Quando a seção que contém o componente Etapa de assinatura é renderizada, ela exibe uma versão PDF assinável do formulário preenchido. O componente Etapa de assinatura ocupa a largura total disponível para o formulário. É recomendável não ter nenhum outro componente na seção que contém o componente Etapa de assinatura.

Execute as seguintes etapas para configurar o componente Etapa de assinatura:

1. Arraste e solte o componente **[!UICONTROL Etapa de assinatura]** do navegador Componentes para o formulário.
1. Selecione o componente de etapa de assinatura recém-adicionado e toque no ícone **Configurar** ![configurar](assets/configure.png). Ele abre o navegador de propriedades e exibe as propriedades da etapa de assinatura. Configure as seguintes propriedades:

   * **[!UICONTROL Nome]**: Especifique o nome do componente.

   * **[!UICONTROL Título]:** especifique o título exclusivo do componente.
   * **[!UICONTROL Mensagem] do modelo:** especifique a mensagem a ser exibida enquanto o PDF de assinatura estiver sendo carregado. [!DNL Adobe Sign] os serviços levam algum tempo para preparar e carregar um PDF de assinatura.
   * **[!UICONTROL Serviço] de assinatura:** selecione a  **[!DNL Adobe Sign]** opção.

   * **[!UICONTROL Usar componente]** herdado de assinatura eletrônica: Se você estiver usando o respectivo formulário adaptável no  [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), AEM  [!DNL Forms] aplicativo ou se o formulário adaptativo subjacente tiver um componente de assinatura eletrônica herdado, selecione a opção  **Usar** componente de assinatura eletrônica herdado.

   * **[!UICONTROL Configuração]**: Selecione uma configuração ([!DNL Adobe Sign] Cloud Service). A caixa suspensa estará disponível somente se a opção **Usar componente E-sign** herdado estiver ativada.

   * **[!UICONTROL Classe]** CSS: Especifique a classe CSS para o componente.

   Toque no ícone Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para salvar as alterações.

   ![Etapa de assinatura](assets/signature_step_new.png)

   >[!NOTE]
   >
   > * Quando você arrasta e solta o componente **[!UICONTROL Etapa de assinatura]** no formulário, o **[!UICONTROL O assinante e a pessoa que preenche o formulário são os mesmos?]** é automaticamente definida como  **Sim**. É necessário manter o formulário funcionando.
      >
      > 
   * Use o componente Etapa de resumo após o componente Etapa de assinatura para obter a melhor experiência. A etapa Resumo envia automaticamente e imediatamente o formulário depois que você conclui a assinatura de um formulário no componente Etapa de assinatura. Se você não usar a etapa de resumo, uma submissão automática será acionada somente após o intervalo definido usando o [Adobe Sign Configuration Service](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).
      > Algumas práticas recomendadas são:
   > * O painel de formulário adaptável que contém a etapa Assinatura está sempre no último ou no segundo painel de um formulário adaptável. Ele pode ser o segundo painel somente quando o último painel contiver a etapa Resumo.
   > * O painel que contém o componente da etapa Assinatura ou Resumo não pode conter nenhum outro componente.
   > * Formulários adaptáveis que contêm Etapa de assinatura não podem ter o botão Enviar. O envio é realizado por meio de um serviço em segundo plano ou da etapa Resumo.
   > * Projete o formulário para não permitir que um usuário navegue de volta de um painel que contém a etapa Assinatura ou Resumo.



### Configure a página de agradecimento ou o componente de etapa de resumo {#configure-the-thank-you-page-or-summary-step-component}

O componente **Etapa de resumo** envia automaticamente o formulário, preenche as informações dentro da página de Resumo personalizada e exibe o resumo do formulário enviado. Ele também obtém as informações necessárias no mapa de retorno. O componente Etapa de resumo ocupa a largura total disponível para o formulário. É recomendável não ter nenhum outro componente na seção que contenha o componente de Etapa de resumo.

Agora, a experiência de assinatura no formulário está pronta. Você pode pré-visualização o formulário para verificar a experiência de assinatura.

## Perguntas frequentes {#frequently-asked-questions}

**P:** É possível incorporar um formulário adaptável em outro formulário adaptável. O formulário adaptativo incorporado pode ser [!DNL Adobe Sign] ativado?
**Ans:** Não, AEM  [!DNL Forms] não suporta o uso de um formulário adaptável que incorpora um formulário adaptativo  [!DNL Adobe Sign] habilitado para assinatura

**P:** Quando eu crio um formulário adaptável usando o modelo avançado e o abro para edição, uma mensagem de erro &quot;Assinatura eletrônica ou signatários não estão configurados corretamente.&quot; é exibido. Como resolver a mensagem de erro?
**Ans:O formulário** adaptativo criado usando o modelo avançado está configurado para uso  [!DNL Adobe Sign]. Para resolver o erro, crie e selecione uma configuração de nuvem [!DNL Adobe Sign] e configure um assinante [!DNL Adobe Sign] para o formulário adaptável.

**P:** Posso usar tags de  [!DNL Adobe Sign] texto em um componente de texto estático de um formulário adaptável?
**Ans:** Sim, você pode usar tags de texto em um componente de texto para adicionar  [!DNL Adobe Sign] campos a um  [Documento de formulário adaptável habilitado para Gravar](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)  (documento gerado automaticamente somente da opção de registro). Para saber mais sobre o procedimento e as regras para criar uma tag de texto, consulte [Documentação do Adobe Sign](https://helpx.adobe.com/sign/using/text-tag.html). Observe também que os formulários adaptativos têm suporte limitado para tags de texto. Você pode usar as tags de texto para criar apenas os campos compatíveis com [Adobe Sign Block](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form).

**P:** AEM  [!DNL Forms] fornece componentes de etapa de assinatura e  [!UICONTROL bloqueio ] Adobe Sign. Eles podem ser usados simultaneamente em uma forma adaptativa?
**Ans:** É possível usar ambos os componentes simultaneamente em um formulário. Estas são algumas recomendações para o uso desses componentes:

**Adobe Sign Block:** você pode usar o  [!UICONTROL Adobe Sign ] Blockpara adicionar  [!UICONTROL Adobe ] Signfields em qualquer lugar do formulário adaptável. Também ajuda a atribuir campos específicos a signatários. Quando um formulário adaptável é visualizado ou publicado, o bloco [!UICONTROL Adobe Sign] não está visível, por padrão. Esses blocos são ativados somente no documento de assinatura. No documento de assinatura, somente os campos atribuídos a um assinante são ativados. [!UICONTROL Os ] Sinalizadores de Adobe podem ser usados com o primeiro e os signatários subsequentes.

**Componente de etapa de assinatura:** você pode usar o componente de etapa de assinatura para criar uma experiência de assinatura no formulário. Ela permite que somente o primeiro assinante assine enquanto o formulário está sendo preenchido. Quando a seção que contém o componente Etapa de assinatura é renderizada, exibe uma versão PDF assinável do formulário. Geralmente, é a última ou penúltima seção seguida do componente de resumo de um formulário.

## Solução de problemas {#troubleshoot}

### [!DNL Adobe Sign] falhas de acordo  {#adobe-sign-agreement-failures}

**ProblemaQuando o**
serviço é configurado para um formulário adaptável, o serviço falha ao criar um  [!DNL Adobe Sign]   [!DNL Adobe Sign] contrato para o formulário adaptativo subjacente.

**Resolução**

* Verifique a configuração [do serviço de nuvem Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md) usada no formulário adaptável.
* Certifique-se de que o aplicativo de API no servidor [!DNL Adobe Sign] usado para configurar o serviço de nuvem [!DNL Adobe Sign] tenha as permissões necessárias.
* Se você estiver usando vários [!DNL Adobe Sign] serviços em nuvem, aponte o **[!UICONTROL URL do oAuth]** de todos os serviços para o mesmo **[!UICONTROL Adobe Sign Shard]**.

* Use endereços de email separados para configurar a conta [!DNL Adobe Sign] e para o primeiro assinante e único assinante. O endereço de email do primeiro assinante ou do único assinante (no caso do assinante único) não pode ser idêntico à conta [!DNL Adobe Sign] usada para configurar os serviços em nuvem do AEM.

### O fluxo de trabalho AEM [!DNL Forms] configurado para um formulário adaptativo habilitado para [!DNL Adobe Sign] não start {#adobe-sign-aem-form-workflow-failures}

**Problema**
Quando  [!DNL Adobe Sign] está configurado para um formulário adaptável, o fluxo de trabalho configurado usando a opção Chamar  [!DNL Forms] fluxo de trabalho não é start.

**Resolução**

* Quando você usa [!DNL Adobe Sign] sem a etapa Assinatura ou o formulário requer assinaturas de várias pessoas, AEM servidor [!DNL Forms] aguarda o scheduler para confirmar se todas as pessoas assinaram o formulário. O scheduler envia o formulário adaptável somente depois que toda a pessoa concluir a assinatura e os start do fluxo de trabalho somente após o envio bem-sucedido do formulário adaptável. Você pode encurtar o intervalo do [scheduler](adobe-sign-integration-adaptive-forms.md) para verificar o status da assinatura do formulário em intervalos rápidos e apertar o envio do formulário.


## Artigos relacionados {#related-articles}

* [Integrar o Adobe Sign ao AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Uso do Adobe Sign em um formulário adaptável](../../forms/using/working-with-adobe-sign.md)
* [Uso do Adobe Sign com AEM Forms (Vídeo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
