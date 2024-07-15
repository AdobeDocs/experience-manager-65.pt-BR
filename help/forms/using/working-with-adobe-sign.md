---
title: Uso do Adobe Sign em um formulário adaptável
description: Habilite fluxos de trabalho de assinatura eletrônica (Adobe Sign) para um formulário adaptável para automatizar fluxos de trabalho de assinatura, simplificar processos de assinatura única e multiassinatura e assinar eletronicamente formulários de dispositivos móveis.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms,Foundation Components,Acrobat Sign
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
exl-id: a8decba9-229d-40a2-992a-3cc8ebefdd6d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '3875'
ht-degree: 0%

---

# Usando [!DNL Adobe Sign] em um formulário adaptável{#using-adobe-sign-in-an-adaptive-form}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html?lang=pt-br) |
| AEM 6.5 | Este artigo |


[!DNL Adobe Sign] habilita fluxos de trabalho de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os fluxos de trabalho para processar documentos para áreas jurídicas, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muito mais.

Em um cenário típico de formulários adaptáveis do [!DNL Adobe Sign], um usuário preenche um formulário adaptável para solicitar um serviço. Por exemplo, um pedido de hipoteca e cartão de crédito requer assinaturas legais de todos os mutuários e corequerentes. Para habilitar fluxos de trabalho de assinatura eletrônica para cenários semelhantes, você pode integrar o [!DNL Adobe Sign] ao AEM [!DNL Forms]. Alguns outros exemplos são, você pode usar [!DNL Adobe Sign] para:

* Feche negócios de qualquer dispositivo com processos totalmente automatizados de propostas, cotações e contratos.
* Conclua os processos de Recursos humanos com mais rapidez e ofereça aos seus funcionários as experiências digitais.
* Reduza os tempos de ciclo do contrato e integre seus fornecedores mais rapidamente.
* Crie fluxos de trabalho digitais que automatizam processos comuns.

A integração do [!DNL Adobe Sign] com o AEM [!DNL Forms] oferece suporte para:

* Workflows de assinatura de um ou vários usuários
* Workflows de assinatura sequencial e simultânea
* Experiências de assinatura no formulário e fora do formulário
* Assinatura de formulários como usuário anônimo ou conectado
* Processos de assinatura dinâmicos (integração com o fluxo de trabalho AEM [!DNL Forms])
* Autenticação por meio de uma base de conhecimento, telefone e perfis sociais

Conheça as [práticas recomendadas de uso do Adobe Sign com formulários adaptáveis](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684) para criar melhores experiências de assinatura.

## Pré-requisitos {#prerequisites}

Antes de usar [!DNL Adobe Sign] em um formulário adaptável:

* Verifique se o serviço de nuvem AEM [!DNL Forms] está configurado para usar [!DNL Adobe Sign]. Para obter detalhes, consulte [Integrar o Adobe Sign com o AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* Mantenha a lista de signatários pronta. Você precisa de pelo menos um endereço de email para cada signatário.

## Configurar [!DNL Adobe Sign] para um formulário adaptável {#configure-adobe-sign-for-an-adaptive-form}

Execute as seguintes etapas para configurar o [!DNL Adobe Sign] para um formulário adaptável:

1. [Editar propriedades do formulário adaptável para o sinal de Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Adicionar campos do Adobe Sign a um formulário adaptável](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Ativar o Adobe Sign para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Selecione Adobe Sign Cloud Service para obter um formulário adaptável](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Adicionar signatários do Adobe Sign a um formulário adaptável](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Selecione Enviar ação para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Detalhes do signatário](assets/signer_details_new.png)

### Editar propriedades de formulário adaptável para [!DNL Adobe Sign] {#enableadobesign}

Configure as propriedades do formulário adaptável para [!DNL Adobe Sign] para um formulário adaptável existente ou novo.

[Criar um formulário adaptável para o Adobe Sign](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) descreve as etapas para criar um formulário adaptável básico. Consulte [Criando um formulário adaptável](../../forms/using/creating-adaptive-form.md) para obter outras opções disponíveis ao criar um formulário adaptável.

#### Criar um formulário adaptável para [!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}

Execute as seguintes etapas para criar um formulário adaptável habilitado para assinatura:

1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione **[!UICONTROL Criar]** e selecione **[!UICONTROL Formulário adaptável]**. Uma lista de modelos é exibida. Selecione o modelo e selecione **[!UICONTROL Próximo]**.
1. Na guia **[!UICONTROL Básico]**:

   1. Especifique o **[!UICONTROL Nome]** e o **[!UICONTROL Título]** para o formulário adaptável.

   1. Selecione o [contêiner de configuração](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) criado ao configurar [!DNL Adobe Sign] com AEM [!DNL Forms].

      >[!NOTE]
      >
      >A lista suspensa **[!UICONTROL Adobe Sign Cloud Service]** exibe os serviços de nuvem configurados no contêiner de configuração selecionado neste campo. A lista suspensa **[!UICONTROL Adobe Sign Cloud Service]** está disponível na seção **[!UICONTROL Assinatura Eletrônica]** das propriedades do formulário adaptável ao selecionar a opção **[!UICONTROL Habilitar Adobe Sign]**.

1. Na guia **[!UICONTROL Modelo de Formulário]**, selecione uma das seguintes opções:

   * Selecione a opção **[!UICONTROL Associar modelo de formulário como o documento de modelo de registro]** e selecione um documento de modelo de registro. Se você usar um modelo de formulário com base no formulário adaptável, os documentos enviados para assinatura exibirão apenas os campos que se baseiam no modelo de formulário associado. Ele não exibe todos os campos do formulário adaptável.

   * Selecione a opção **[!UICONTROL Gerar documento de registro]**. Se você usar um formulário adaptável com a opção Documento de registro ativada, o documento enviado para assinatura exibirá todos os campos do formulário adaptável.

1. Selecione **[!UICONTROL Criar.]** Um formulário adaptável habilitado para assinatura é criado, que pode ser usado para adicionar [!DNL Adobe Sign] campos.

#### Editar um formulário adaptável para [!DNL Adobe Sign] {#editafsign}

Execute as seguintes etapas para usar [!DNL Adobe Sign] em um formulário adaptável existente:

1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione o formulário adaptável e selecione **[!UICONTROL Propriedades]**.
1. Na guia **[!UICONTROL Básico]**, selecione o [contêiner de configuração](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) criado ao configurar o [!DNL Adobe Sign] com AEM [!DNL Forms].
1. Na guia **[!UICONTROL Modelo de Formulário]**, selecione uma das seguintes opções:

   * Selecione a opção **[!UICONTROL Associar modelo de formulário como o documento de modelo de registro]** e selecione um documento de modelo de registro. Se você usar um modelo de formulário com base no formulário adaptável, os documentos enviados para assinatura exibirão apenas os campos que se baseiam no modelo de formulário associado. Ele não exibe todos os campos do formulário adaptável.

   * Selecione a opção **[!UICONTROL Gerar documento de registro]**. Se você usar um formulário adaptável com a opção Documento de registro ativada, o documento enviado para assinatura exibirá todos os campos do formulário adaptável.

1. Selecione **[!UICONTROL Salvar e fechar]**. O formulário adaptável está habilitado para [!DNL Adobe Sign].

### Adicionar campos do Adobe Sign a um formulário adaptável {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] tem vários campos que podem ser colocados em um formulário adaptável. Esses campos aceitam vários tipos de dados, como assinaturas, iniciais, empresa ou título e ajudam a coletar informações adicionais durante a assinatura, juntamente com as assinaturas. Você pode usar o componente de Bloco [!DNL Adobe Sign] para colocar campos [!DNL Adobe Sign] em vários locais em um formulário adaptável.

Execute as seguintes etapas para adicionar campos a um formulário adaptável e personalizar várias opções relacionadas a esses campos:

1. Arraste e solte o componente **[!UICONTROL Bloco de Adobe Sign]** do navegador de componentes no formulário adaptável. O componente de Bloqueio [!DNL Adobe Sign] tem todos os campos [!DNL Adobe Sign] com suporte. Por padrão, ele adiciona um campo **Assinatura** ao formulário adaptável.

   ![Bloco de assinatura](assets/sign_block_new.png)

   Por padrão, o Bloco [!DNL Adobe Sign] não fica visível no formulário adaptável publicado. É visível apenas nos documentos de assinatura. Você pode alterar a visibilidade do Bloco [!DNL Adobe Sign] das propriedades do componente de Bloco [!DNL Adobe Sign].

   >[!NOTE]
   >
   >    * O uso do bloco [!DNL Adobe Sign] não é obrigatório para usar [!DNL Adobe Sign] em um formulário adaptável. Se você não usar o bloco [!DNL Adobe Sign] e adicionar campos para os signatários, o campo de assinatura padrão será exibido na parte inferior dos documentos de assinatura.
   >    * Use o bloco [!DNL Adobe Sign] somente para os formulários adaptáveis que geram automaticamente o Documento de registro. Se você estiver usando um XDP personalizado para gerar um Documento de registro ou um formulário adaptável baseado em modelo de formulário, o bloco [!DNL Adobe Sign] não será suportado.
   >
   >

1. Selecione o componente de **[!UICONTROL Bloco do Adobe Sign]** e selecione o ícone **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png). Ele exibe opções para adicionar campos e a aparência do formato de um campo.

   ![campos de seleção de bloco de assinatura da adobe](assets/adobe-sign-block-select-fields.png)

   **A.** Selecione e adicione [!DNL Adobe Sign] campos. **B.** Expanda o bloco [!DNL Adobe Sign] para exibição em tela inteira

1. Selecione o ícone do **[!UICONTROL Campo do Adobe Sign]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png). Ele exibe opções para selecionar e adicionar [!DNL Adobe Sign] campos.

   Expanda o campo suspenso **[!UICONTROL Tipo]** para selecionar um campo [!DNL Adobe Sign] e selecione o ícone Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para adicionar o campo selecionado ao bloco [!DNL Adobe Sign]. O campo suspenso **[!UICONTROL Tipo]** inclui os tipos de campo Assinatura, Informações do signatário e Dados. A integração [!DNL Adobe Sign] com AEM [!DNL Forms] oferece suporte aos campos listados somente na caixa suspensa [!UICONTROL Tipo]. Para obter informações detalhadas sobre os campos [!DNL Adobe Sign], consulte a [documentação do Adobe Sign](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   É obrigatório fornecer um nome exclusivo para um campo. Você também pode selecionar a opção obrigatório para marcar um campo. Além das opções **[!UICONTROL Nome]** e **[!UICONTROL Obrigatório]**, alguns campos [!DNL Adobe Sign] têm mais opções. Por exemplo, máscara e várias linhas. Além disso, especifique nomes exclusivos para cada campo [!DNL Adobe Sign], sejam os campos que residem no mesmo bloco [!DNL Adobe Sign] ou em blocos  diferentes.

   Se você selecionar **[!UICONTROL Assinatura digital]** na lista suspensa, poderá aplicar assinaturas digitais ao formulário adaptável:

   * Online usando assinaturas em nuvem para assinar com uma [ID digital](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) hospedada por um provedor de serviços de confiança.
   * Localmente, baixando o documento com Adobe Acrobat ou Reader usando um cartão inteligente, token USB ou ID digital baseada em arquivo.

### Habilitar [!DNL Adobe Sign] para um formulário adaptável {#enableadobsignforanadaptiveform}

Pronto para uso, o [!DNL Adobe Sign] não está habilitado para um formulário adaptável. Execute as seguintes etapas para ativá-la:

1. No Navegador de conteúdo, selecione **[!UICONTROL Contêiner de formulário]** e selecione o ícone **[!UICONTROL Configurar]** ![configurar](assets/configure.png). Ela abre as propriedades do navegador e exibe as propriedades do contêiner do Formulário adaptável.
1. No navegador de propriedades, expanda a opção **[!UICONTROL Assinatura eletrônica]** e selecione a opção **[!UICONTROL Habilitar Adobe Sign]**. Ele habilita [!DNL Adobe Sign] para um formulário adaptável.

### Selecionar Cloud Service [!DNL Adobe Sign] e ordem de assinatura {#selectadobesigncloudserviceforanadaptiveform}

Você pode configurar vários serviços do [!DNL Adobe Sign] para uma instância de AEM [!DNL Forms]. É aconselhável ter um conjunto separado de serviços para cada função (Recursos Humanos, Finanças e muito mais). Isso facilita o rastreamento e os relatórios de documentos assinados. Por exemplo, um banco tem vários departamentos. Você pode ter uma configuração separada para cada departamento para um melhor rastreamento dos documentos.

Um documento também pode ter vários signatários. Por exemplo, uma solicitação de cartão de crédito pode ter vários candidatos. Um banco requer assinaturas de todos os candidatos antes de iniciar o processamento da solicitação. Para cenários com vários signatários, você pode optar por assinar o documento em ordem sequencial ou simultânea.

Execute as seguintes etapas para selecionar um serviço em nuvem e a ordem de assinatura:

![serviço-nuvem](assets/cloud-service.png)

1. No Navegador de conteúdo, selecione **[!UICONTROL Contêiner de formulário]** e selecione o ícone **[!UICONTROL Configurar]** ![configurar](assets/configure.png). Ela abre as propriedades do navegador e exibe as propriedades do contêiner do Formulário adaptável.
1. No navegador de propriedades, expanda a opção **[!UICONTROL Assinatura eletrônica]** e selecione a opção **[!UICONTROL Habilitar Adobe Sign]**. Ele habilita [!DNL Adobe Sign] para um formulário adaptável.
1. Selecione um serviço de nuvem na lista já configurada de [!DNL Adobe Sign] Cloud Service.

   Se a lista **[!UICONTROL Adobe Sign Cloud Service]** estiver vazia, siga o artigo [Configurar Adobe Sign com AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) para configurar o serviço.

   A lista suspensa lista os serviços de nuvem existentes na pasta `global` em Ferramentas > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]**. Além disso, a lista suspensa também lista os serviços de nuvem que existem na pasta selecionada no campo **[!UICONTROL Contêiner de configuração]** ao criar um formulário adaptável.

1. Selecione a ordem de assinatura na caixa de diálogo **[!UICONTROL Os signatários podem assinar]**. [!DNL Adobe Sign] cantores podem assinar um formulário adaptável **[!UICONTROL Sequencialmente]** - um após o outro signatário ou **[!UICONTROL Simultaneamente]** - em qualquer ordem.

   Em ordem sequencial, um signatário recebe o formulário para assinatura de cada vez. Depois que um signatário concluir a assinatura do documento, o formulário será enviado para o próximo signatário e assim por diante.

   Em ordem simultânea, vários signatários podem assinar um formulário de cada vez.

1. [Adicionar signatários a um formulário adaptável](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) e selecione o ícone Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para salvar as alterações.


### Adicionar signatários a um formulário adaptável {#addsignerstoanadaptiveform}

Você pode ter apenas um ou vários signatários para um formulário adaptável. Ao adicionar um signatário, você também pode configurar os detalhes de autenticação do signatário. Você também pode selecionar se o preenchimento do formulário e o cantor são a mesma pessoa. Execute as seguintes etapas para adicionar e fornecer vários detalhes sobre um signatário:

1. No Navegador de conteúdo, selecione **[!UICONTROL Contêiner de formulário]** e selecione o ícone **[!UICONTROL Configurar]** ![configurar](assets/configure.png). Ela abre o navegador de propriedades com as propriedades do contêiner do Formulário adaptável.
1. No navegador de propriedades, expanda a opção **[!UICONTROL Assinatura eletrônica]** e selecione a opção **[!UICONTROL Habilitar Adobe Sign]**. Ele habilita [!DNL Adobe Sign] para um formulário adaptável.
1. Selecione **[!UICONTROL Adicionar signatário]** em **[!UICONTROL Configuração do signatário]**. Ele adiciona um signatário ao formulário adaptável. Você pode adicionar vários signatários do [!DNL Adobe Sign] a um formulário adaptável.
   ![detalhes do telefone](assets/phone-details.png)

1. Clique no ícone **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png) para especificar as seguintes informações sobre o signatário:

   * **[!UICONTROL Título]:** especifique um título para identificar exclusivamente um signatário.

   * **[!UICONTROL O signatário e a pessoa que preenche o formulário são a mesma pessoa?]:** Selecione **Sim**, se o preenchimento do formulário e o primeiro signatário forem a mesma pessoa. Se a opção estiver definida como **Não**, não use o componente de etapa de assinatura no formulário adaptável. Se o formulário contiver um componente Etapa de assinatura, o campo será automaticamente definido como Sim.

   * **[!UICONTROL Endereço de email do signatário]:** Especifique o endereço de email do signatário. O signatário recebe para ser assinados documentos/formulários no endereço de email especificado. Você pode optar por usar um endereço de email fornecido em um campo de formulário, no perfil de usuário AEM do usuário conectado ou inserir manualmente um endereço de email. É uma etapa obrigatória. Verifique se o endereço de email do primeiro signatário ou do único signatário (se houver um único signatário) não é idêntico à conta do [!DNL Adobe Sign] usada para configurar os serviços em nuvem do AEM.

   * **[!UICONTROL Método de Autenticação do Assinante]:** Especifique o método para autenticar um usuário antes de abrir um formulário para assinatura. Você pode escolher entre telefone, base de conhecimento e autenticação com base na identidade social. Para o Adobe Acrobat Sign Solutions for Government, somente as opções de autenticação por telefone e com base em conhecimento estão disponíveis.

   >[!NOTE]
   >
   >    * Por padrão, a autenticação com base na identidade social fornece uma opção para autenticar usando o Facebook, o Google e o LinkedIn. Você pode contatar o suporte do [!DNL Adobe Sign] para habilitar outros provedores de autenticação social.
   >
   >

   * **[!DNL Adobe Sign]campos para preencher ou assinar:** Selecione [!DNL Adobe Sign] campos para o signatário. Um formulário adaptável pode ter vários campos [!DNL Adobe Sign]. Você pode optar por ativar campos específicos para um signatário. O campo exibe todos os [!DNL Adobe Sign] Blocos disponíveis. Ao selecionar um bloco, todos os campos do bloco são selecionados. Você pode usar o ícone X para desmarcar um campo.

   ![detalhes do signatário](assets/signer-details.png)

   A imagem acima tem dois exemplos de [!DNL Adobe Sign] Blocos: Personal-Information e Office-details

   Selecione o ícone Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). O signatário é adicionado e configurado.

### Selecione Enviar ação para um formulário adaptável {#selectsubmitactionforanadaptiveform}

Depois de adicionar [!DNL Adobe Sign] campos a um formulário adaptável, habilitar [!DNL Adobe Sign] no contêiner de formulário, selecionar [!DNL Adobe Sign] Cloud Service e adicionar [!DNL Adobe Sign] signatários, selecione uma ação de envio apropriada para o formulário adaptável. Para obter informações detalhadas sobre ações de envio de formulários adaptáveis, consulte [Configurar a ação Enviar](../../forms/using/configuring-submit-actions.md).

Além disso, um formulário adaptável habilitado para [!DNL Adobe Sign] é enviado somente depois que todos os signatários assinarem o formulário. Você pode encontrar o formulário parcialmente assinado na seção Pending Sign do portal de formulários. O Serviço de Configuração [!DNL Adobe Sign] continua sondando o servidor [!DNL Adobe Sign] em [intervalos regulares](../../forms/using/adobe-sign-integration-adaptive-forms.md) para verificar o status das assinaturas. Se todos os signatários concluírem a assinatura do formulário, o serviço de ação de envio será iniciado e o formulário será enviado. Se você estiver usando uma ação de envio personalizada e o formulário usar [!DNL Adobe Sign], atualize sua ação de envio personalizada para usar o serviço de ação de envio.

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. Use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

Sua experiência de assinatura de formulário está pronta. Você pode visualizar o formulário para verificar a experiência de assinatura. No formulário publicado, os campos de Bloqueio [!DNL Adobe Sign] são exibidos quando um signatário recebe o formulário para assinar por email. Essa experiência também é conhecida como experiência de assinatura fora de formulário. Você também pode configurar uma experiência de assinatura no formulário para o primeiro signatário. Para obter etapas detalhadas, consulte [Criar experiência de assinatura no formulário](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## Configurar assinaturas em nuvem para um formulário adaptável {#configure-cloud-signatures-for-an-adaptive-form}

As assinaturas digitais ou remotas baseadas em nuvem são uma nova geração de assinaturas digitais que funcionam no desktop, nos dispositivos móveis e na Web — e atendem aos mais altos níveis de conformidade e garantia para autenticação de assinante. Você pode assinar um formulário adaptável com assinaturas digitais baseadas em nuvem.

Depois de [editar as propriedades do formulário adaptável para o sinal de Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign), execute as seguintes etapas para adicionar o campo de assinatura em nuvem a um formulário adaptável:

1. Arraste e solte o componente **[!UICONTROL Bloco de Adobe Sign]** do navegador de componentes no formulário adaptável. O componente [!UICONTROL Bloco de Adobe Sign] tem todos os campos [!DNL Adobe Sign] com suporte. Por padrão, ele adiciona um campo **[!UICONTROL Assinatura]** ao formulário adaptável.

   ![Bloco de assinatura](assets/sign-block-new.png)

1. Selecione o componente de **[!UICONTROL Bloco do Adobe Sign]** e selecione o ícone **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png). Ele exibe opções para adicionar campos e a aparência do formato de um campo.

   ![campos de seleção de bloco de assinatura da adobe](assets/adobe-sign-block-select-fields.png)

   **A.** Selecione e adicione [!DNL Adobe Sign] campos. **B.** Expanda o bloco [!DNL Adobe Sign] para exibição em tela inteira

1. Selecione o ícone do **[!UICONTROL Campo do Adobe Sign]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png). Ele exibe opções para selecionar e adicionar [!DNL Adobe Sign] campos.

   Expanda o campo suspenso **[!UICONTROL Tipo]** para selecionar **[!UICONTROL Assinatura Digital]** e selecione o ícone **Concluído** para adicionar o campo selecionado ao bloco [!DNL Adobe Sign].

   ![Assinaturas digitais](assets/digital_signatures_new.png)

   É obrigatório fornecer um nome exclusivo para um campo.

   Aplique assinaturas digitais ao formulário adaptável usando:

   * Assinaturas na nuvem: assine com uma [ID digital](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) hospedada por um provedor de serviços de confiança. A opção Assinatura na nuvem não está disponível para o Adobe Acrobat Sign Solutions para o governo.

   * Adobe Acrobat ou Reader: baixe e abra o documento com o Adobe Acrobat ou Reader para assinar usando um cartão inteligente, token USB ou ID digital baseada em arquivo.

   Depois de adicionar o campo de assinatura em nuvem ao formulário adaptável, execute as seguintes etapas para concluir o processo de configuração:

   * [Ativar o Adobe Sign para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Selecione Adobe Sign Cloud Service para obter um formulário adaptável](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Adicionar signatários do Adobe Sign a um formulário adaptável](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Selecione Enviar ação para um formulário adaptável](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

## Criar experiência de assinatura no formulário {#create-in-form-signing-experience}

Um usuário também pode assinar um formulário adaptável ao preencher o formulário. Essa experiência também é conhecida como experiência de assinatura no formulário. A experiência de assinatura no formulário está disponível apenas para o primeiro cantor em um ambiente com vários signatários. Execute as seguintes etapas para criar uma experiência de assinatura no formulário para um formulário adaptável:

1. [Adicionar e configurar o componente da Etapa de Assinatura](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. [Adicionar o componente da Etapa de Resumo](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component).

![Experiência de assinatura no formulário](assets/in_form_signing_experience_new.png)

### Adicionar e configurar o componente Etapa de assinatura {#add-and-configure-the-signature-step-component}

Use o componente Etapa de assinatura para fornecer uma área para assinar eletronicamente o formulário preenchido. Quando a seção que contém o componente Etapa de assinatura é renderizada, ela exibe uma versão de PDF assinável do formulário preenchido. O componente Etapa de assinatura ocupa toda a largura disponível para o formulário. É recomendável não ter nenhum outro componente na seção que contém o componente Etapa de assinatura.

Execute as seguintes etapas para configurar o componente Etapa de assinatura:

1. Arraste e solte o componente **[!UICONTROL Etapa de assinatura]** do navegador Componentes no formulário.
1. Selecione o componente da etapa de Assinatura recém-adicionado e selecione o ícone **Configurar** ![configurar](assets/configure.png). Ele abre o navegador de propriedades e exibe as propriedades da etapa Assinatura. Configure as seguintes propriedades:

   * **[!UICONTROL Nome]**: especifique o nome do componente.

   * **[!UICONTROL Título]:** especifique o título exclusivo do componente.
   * **[!UICONTROL Mensagem de modelo]:** especifique a mensagem a ser exibida enquanto o PDF de assinatura estiver sendo carregado. Os serviços do [!DNL Adobe Sign] demoram algum tempo para preparar e carregar o PDF de assinatura.
   * **[!UICONTROL Serviço de assinatura]:** Selecione a opção **[!DNL Adobe Sign]**.

   * **[!UICONTROL Usar componente E-sign herdado]**: se você estiver usando o respectivo formulário adaptável no aplicativo [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), AEM [!DNL Forms] ou se o formulário adaptável subjacente tiver componente e-sign herdado, selecione a opção **Usar componente E-sign herdado**.

   * **[!UICONTROL Configuração]**: selecione uma configuração ([!DNL Adobe Sign] Cloud Service). A caixa suspensa só estará disponível se a opção **Usar componente E-sign herdado** estiver habilitada.

   * **[!UICONTROL Classe CSS]**: especifique a classe CSS para o componente.

   Selecione o ícone Concluído ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para salvar as alterações.

   ![Etapa de assinatura](assets/signature_step_new.png)

   >[!NOTE]
   >
   >* Ao arrastar e soltar o componente **[!UICONTROL Etapa de assinatura]** no formulário, o **[!UICONTROL Signatário e a pessoa que preenche o formulário são a mesma pessoa?A opção]** é automaticamente definida como **Sim**. É necessário manter o formulário funcionando.
   >* Use o componente Etapa de resumo após o componente Etapa de assinatura para obter a melhor experiência. A etapa Resumo envia o formulário automática e imediatamente após você concluir a assinatura de um formulário no componente Etapa de assinatura. Se você não usar a etapa de resumo, um envio automático será acionado somente após o intervalo definido com o [Serviço de Configuração do Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).
   >
   >Algumas práticas recomendadas são:
   >
   >* O painel Formulário adaptável que contém a etapa Assinatura está sempre no último ou no segundo último painel de um formulário adaptável. Ele pode ser o segundo último painel somente quando o último painel contém a etapa Resumo.
   >* O painel que contém o componente da etapa Assinatura ou Resumo não pode conter nenhum outro componente.
   >* Os formulários adaptáveis que contêm a Etapa de assinatura não podem ter o botão enviar.
   >* O envio para os formulários adaptáveis que contêm a etapa Assinatura é feito por meio de um serviço em segundo plano ou da etapa Resumo. Se houver um signatário configurado que também esteja preenchendo o formulário, a vantagem de lidar com o envio do formulário adaptável usando a etapa Resumo é que ele avalia imediatamente se o signatário assinou o formulário e invoca a ação de envio. Um serviço em segundo plano leva mais tempo para avaliar se todos os signatários configurados assinaram o formulário e atrasa o envio do formulário adaptável.
   >* Crie o formulário para não permitir que um usuário volte de um painel que contém a etapa Assinatura ou Resumo.


### Configurar a página de agradecimento ou o componente da etapa de resumo {#configure-the-thank-you-page-or-summary-step-component}

O componente **Etapa de resumo** envia automaticamente o formulário, preenche as informações dentro da página de resumo personalizada e exibe o resumo do formulário enviado. Ele também obtém as informações necessárias no mapa de retorno. O componente Etapa de resumo ocupa toda a largura disponível para o formulário. É recomendável não ter nenhum outro componente na seção que contém o componente Etapa de resumo.

Agora, a experiência de assinatura no formulário está pronta. Você pode visualizar o formulário para verificar a experiência de assinatura.

## Perguntas frequentes {#frequently-asked-questions}

**P:** Você pode incorporar um formulário adaptável em outro formulário adaptável. O formulário adaptável inserido pode ser habilitado para [!DNL Adobe Sign]?
**Ans:** Não, AEM [!DNL Forms] não oferece suporte ao uso de um formulário adaptável que incorpora um formulário adaptável habilitado para assinatura com o [!DNL Adobe Sign]

**P:** Quando eu criar um formulário adaptável usando o modelo avançado e abri-lo para edição, uma mensagem de erro &quot;Assinatura eletrônica ou assinantes não estão configurados corretamente.&quot; é exibida. Como resolver a mensagem de erro?
**Ans:** O formulário adaptável criado com o modelo avançado está configurado para usar [!DNL Adobe Sign]. Para resolver o erro, crie e selecione uma configuração de nuvem [!DNL Adobe Sign] e configure um signatário [!DNL Adobe Sign] para o formulário adaptável.

**P:** Posso usar [!DNL Adobe Sign] marcas de texto em um componente de texto estático de um formulário adaptável?
**Ans:** Sim, você pode usar marcas de texto em um componente de texto para adicionar campos [!DNL Adobe Sign] a um [Documento de Registro](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) (somente opção de documento de registro gerado automaticamente) formulário adaptável habilitado. Para saber mais sobre o procedimento e as regras para criar uma marca de texto, consulte a [Documentação do Adobe Sign](https://helpx.adobe.com/sign/using/text-tag.html). Observe também que os formulários adaptáveis têm suporte limitado para tags de texto. Você pode usar as marcas de texto para criar apenas os campos aceitos pelo [Bloco Adobe Sign](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form).

**Q:** AEM [!DNL Forms] fornece componentes de etapa de [!UICONTROL Bloco Adobe Sign] e Assinatura. Eles podem ser usados simultaneamente em um formulário adaptável?
**Ans:** Você pode usar ambos os componentes simultaneamente em um formulário. Estas são algumas recomendações para usar esses componentes:

**Bloco do Adobe Sign:** Você pode usar o [!UICONTROL Bloco do Adobe Sign] para adicionar campos do [!UICONTROL Adobe Sign] em qualquer lugar do formulário adaptável. Também ajuda a atribuir campos específicos aos signatários. Quando um formulário adaptável é visualizado ou publicado, o Bloco [!UICONTROL Adobe Sign] não fica visível, por padrão. Esses blocos são ativados somente no documento de assinatura. No documento de assinatura, somente os campos atribuídos a um signatário são ativados. O bloco [!UICONTROL Adobe Sign] pode ser usado com o primeiro signatário e os subsequentes.

**Componente da etapa de assinatura:** Você pode usar o componente da etapa de assinatura para criar uma experiência de assinatura no formulário. Permite que apenas o primeiro signatário assine enquanto o formulário está sendo preenchido. Quando a seção que contém o componente Etapa de assinatura é renderizada, ela exibe uma versão de PDF assinável do formulário. É geralmente a última ou penúltima seção seguida pelo componente de resumo de um formulário.

## Solução de problemas {#troubleshoot}

### [!DNL Adobe Sign] falhas de contrato {#adobe-sign-agreement-failures}

**Problema**
Quando o serviço [!DNL Adobe Sign] é configurado para um formulário adaptável, o serviço falha ao criar um contrato [!DNL Adobe Sign] para o formulário adaptável subjacente.

**Resolução**

* Verifique a [configuração do Adobe Sign cloud service](../../forms/using/adobe-sign-integration-adaptive-forms.md) usada no formulário adaptável.
* Verifique se o aplicativo de API no servidor [!DNL Adobe Sign] usado para configurar o serviço de Nuvem [!DNL Adobe Sign] tem as permissões necessárias.
* Se você estiver usando vários serviços de Nuvem do [!DNL Adobe Sign], aponte a **[!UICONTROL URL do oAuth]** de todos os serviços para o mesmo **[!UICONTROL Fragmento do Adobe Sign]**.

* Use endereços de email separados para configurar a conta do [!DNL Adobe Sign] e para o primeiro signatário e o signatário único. O endereço de email do primeiro signatário ou do único signatário (se houver um signatário único) não pode ser idêntico à conta do [!DNL Adobe Sign] usada para configurar os serviços em nuvem do AEM.

### O fluxo de trabalho AEM [!DNL Forms] configurado para um formulário adaptável habilitado para [!DNL Adobe Sign] não inicia {#adobe-sign-aem-form-workflow-failures}

**Problema**
Quando [!DNL Adobe Sign] é configurado para um formulário adaptável, o fluxo de trabalho configurado usando a opção Chamar fluxo de trabalho [!DNL Forms] não é iniciado.

**Resolução**

* Quando você usa [!DNL Adobe Sign] sem a etapa Assinatura ou o formulário requer assinaturas de várias pessoas, o servidor AEM [!DNL Forms] aguarda que o agendador confirme que todas as pessoas assinaram o formulário. O scheduler envia o formulário adaptável somente depois que todas as pessoas concluem a assinatura e o fluxo de trabalho começa somente após um envio bem-sucedido do formulário adaptável. Você pode reduzir o intervalo do [scheduler](adobe-sign-integration-adaptive-forms.md) para verificar o status da assinatura do formulário em intervalos rápidos e agilizar o envio do formulário.


## Artigos relacionados {#related-articles}

* [Integrar o Adobe Sign com o AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Práticas recomendadas para usar o Adobe Sign com formulários adaptáveis](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [Usando o Adobe Sign com o AEM Forms (Vídeo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
