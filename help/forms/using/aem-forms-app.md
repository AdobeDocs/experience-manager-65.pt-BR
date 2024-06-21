---
title: aplicativo AEM Forms
description: O aplicativo AEM Forms permite que seus funcionários de campo usem formulários adaptáveis em seus dispositivos móveis.
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 171754a2-1ba5-42dc-b6d2-3d730807cc31
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '2410'
ht-degree: 0%

---

# Introdução ao aplicativo AEM Forms {#aem-forms-app}

## Visão geral {#overview}

O aplicativo AEM Forms permite a sincronização de formulários adaptáveis, formulários móveis e conjuntos de formulários em dispositivos móveis, com base no servidor. Você pode definir workflows que são [Fluxos de trabalho centrados no Forms no OSGi](/help/forms/using/aem-forms-workflow.md) ou fluxos de trabalho do Forms no JEE. Por exemplo, você executa uma empresa bancária e usa o AEM Forms para gerenciar aplicativos e comunicações de clientes. Seus clientes preenchem um formulário e o enviam para verificação. Se você habilitar o formulário em dispositivos móveis, seus clientes poderão preenchê-lo no aplicativo AEM Forms. Você também pode gerenciar o fluxo de trabalho de verificação ativando o formulário de verificação em dispositivos móveis. Seu trabalhador de campo pode transportar um dispositivo móvel para o cliente, verificar os detalhes e enviar o formulário. O aplicativo AEM Forms é sincronizado com o servidor do AEM Forms e busca os formulários habilitados para dispositivos móveis. Se o aplicativo estiver offline, ele armazenará dados localmente.

O código-fonte do aplicativo AEM Forms está disponível para os clientes por meio da Distribuição de software. O pacote de código-fonte na Distribuição de software está disponível como: `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

O aplicativo AEM Forms é compatível com dispositivos iOS, Android e Windows. Você pode instalar o aplicativo AEM Forms para Android do Google Play, iOS do App Store e Windows da Windows Store.

    [![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

Para instalar, personalizar e distribuir o aplicativo em dispositivos iOS, Android ou Windows, consulte [Personalizar, criar e distribuir o aplicativo AEM Forms](#customize-build-distribute).

## Pré-requisitos {#prerequisites}

O aplicativo AEM Forms requer um servidor AEM Forms. Os usuários podem renderizar formulários criados no servidor do AEM Forms, preenchê-los, salvá-los como rascunhos e enviá-los. O aplicativo se conecta ao servidor e obtém formulários habilitados. O aplicativo AEM Forms é sincronizado com o servidor e, assim que os formulários são carregados no aplicativo, os usuários podem trabalhar offline. Se o aplicativo estiver offline, os dados serão salvos no dispositivo e sincronizados com o servidor quando o aplicativo estiver online.

### Aplicativo AEM Forms com servidores usando o AEM Forms Workflow {#aem-forms-app-with-servers-using-aem-forms-workflow}

Se você tiver um servidor do AEM Forms Workflow, poderá renderizar formulários como tarefas no aplicativo AEM Forms. Por exemplo, você executa uma empresa bancária e o cliente preenche um aplicativo para usar seus serviços. O aplicativo é um formulário adaptável que aceita informações de seus clientes e as armazena como um envio para revisão. O administrador revisa um aplicativo e encaminha uma solicitação de verificação ao trabalhador de campo. O aplicativo encaminhado habilita um formulário de verificação no aplicativo do trabalhador de campo como uma tarefa. Seu trabalhador de campo carrega o dispositivo móvel para seu cliente e verifica os detalhes.

### Aplicativo AEM Forms com servidores usando fluxo de trabalho centrado no Forms no OSGi {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

Se você tiver um servidor AEM Forms, poderá renderizar formulários adaptáveis como o aplicativo Caixa de entrada AEM e tarefas no aplicativo AEM Forms. Por exemplo, você executa uma empresa bancária e o cliente preenche um aplicativo para usar seus serviços. O aplicativo é associado a um formulário adaptável que aceita informações de seus clientes e as armazena como um envio para revisão. O administrador revisa a tarefa e aprova a solicitação de verificação ao trabalhador de campo. Seu trabalhador de campo carrega o dispositivo móvel para seu cliente e verifica os detalhes.

### Formulários autônomos ou aplicativo AEM Forms com servidores sem fluxo de trabalho AEM Forms {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

Um servidor do AEM Forms que não usa o AEM Forms Workflow é o AEM Forms no OSGi, um formulário móvel independente ou um formulário adaptável. O aplicativo AEM Forms funciona com sua implementação do AEM Forms no [OSGi](/help/sites-deploying/configuring-osgi.md). O Forms que você habilita e publica para o aplicativo AEM Forms está disponível no seu aplicativo.

Os formulários são baixados no aplicativo e estão disponíveis offline. Por exemplo, você está executando uma empresa bancária e um cliente preenche um aplicativo em seu site. O aplicativo é um formulário adaptável que aceita informações de seus clientes e as armazena para revisão. O administrador revisa o formulário e cria um formulário de verificação na instância de autor do AEM. O administrador habilita a sincronização do formulário com o aplicativo AEM Forms e o publica. Se o formulário de verificação estiver disponível no aplicativo AEM Forms, seu agente de campo poderá usar um dispositivo móvel para verificar os detalhes do cliente. O dispositivo móvel é sincronizado com o servidor e o formulário de verificação é carregado no aplicativo. O agente de campo pode visitar o cliente, verificar os detalhes, salvar dados como rascunho ou enviar o formulário de verificação. O formulário é sincronizado com o servidor sempre que o aplicativo está online.

Para sincronizar o formulário no aplicativo AEM Forms:

1. Na instância do autor, selecione um formulário e clique em **[!UICONTROL Propriedades da exibição]**.

1. Na página de propriedades, clique em **[!UICONTROL Avançado]**.
1. Em Avançado, habilite a opção: **[!UICONTROL Sincronizar com o aplicativo AEM Forms]** e selecione **[!UICONTROL Salvar]**.

Quando o formulário é publicado, o aplicativo é sincronizado com o servidor e busca o formulário. Para sincronizar vários formulários, na instância do autor, selecione vários formulários no gerenciador de formulários e **[!UICONTROL Sincronizar com o aplicativo AEM Forms]**.

## Suporte a dispositivo móvel {#mobile-device-support}

Consulte [Aplicativo AEM Forms (anteriormente conhecido como Espaço de trabalho móvel)](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## Principais recursos do aplicativo AEM Forms {#key-features-of-aem-forms-app}

### aplicativo AEM Forms com servidores AEM Forms {#aem-forms-app-with-aem-forms-servers}

Você pode sincronizar seu aplicativo com o servidor do AEM Forms e trabalhar com formulários em seu dispositivo móvel.

Com o servidor do AEM Forms Workflow, um formulário pode ser associado a um ponto inicial em um processo do workbench e em um aplicativo da Caixa de entrada AEM. Um aplicativo da Caixa de entrada AEM pode ter um formulário adaptável associado a ele. Um ponto inicial pode ter um formulário adaptável, formulário HTML5 ou um conjunto de formulários associado a ele. Um ponto de partida pode ser enviado como uma tarefa ou a tarefa pode ser salva como um rascunho. Para obter mais informações sobre as diferenças entre um aplicativo da Caixa de entrada AEM e um ponto de partida, consulte [Ações e recursos de fluxos de trabalho do AEM centrados em formulários em fluxos de trabalho OSGi e AEM Forms JEE](capabilities-osgi-jee-workflows.md).

Com o servidor do AEM Forms sem fluxo de trabalho do AEM Forms, um formulário habilitado para sincronização no aplicativo é renderizado no aplicativo do AEM Forms. Os Forms estão disponíveis na guia Forms do aplicativo e podem ser enviados ou salvos como rascunho. Formulários adaptáveis e formulários móveis são compatíveis com o aplicativo.

1. **Salvamento de uma tarefa ou formulário como rascunho**

   A opção Salvar como rascunho salva um instantâneo de uma tarefa ou formulário junto com os dados preenchidos e os arquivos anexados no formulário associado. Os rascunhos são salvos no dispositivo móvel e sincronizados com o servidor do AEM Forms para uma recuperação posterior.

   Consulte [Salvamento de uma tarefa ou formulário como rascunho](/help/forms/using/save-as-draft.md).

1. **Salvar formulário como modelo**

   Às vezes, quando os usuários preenchem um formulário, as entradas para alguns campos permanecem as mesmas. Para essas instâncias, é possível preencher os campos que exigem valores idênticos em cada instância e salvar o formulário ou o rascunho como um modelo. Agora, sempre que você criar uma instância do modelo, os campos especificados já estarão preenchidos com os valores especificados no modelo. Ele ajuda a economizar tempo e esforço necessários para preencher o formulário.

   Consulte [Salvar formulários como modelos](/help/forms/using/save-forms-and-start-points-as-templates.md).

### Trabalhar com tarefas e formulários {#working-with-tasks-and-forms}

Você pode sincronizar seu aplicativo com o servidor do AEM Forms Workflow e trabalhar em tarefas e formulários em seu dispositivo móvel.

Uma tarefa no dispositivo móvel contém um formulário adaptável, um formulário HTML5 ou um conjunto de formulários e também pode conter anexos e [URL de resumo](/help/forms/using/getting-task-variables-summary-url.md). Por padrão, as tarefas atribuídas a você são colocadas no **[!UICONTROL Tarefas]** pasta. Ao trabalhar em uma tarefa, você pode alterá-la e salvar uma cópia de rascunho no servidor do AEM Forms.

Um formulário no dispositivo móvel pode ser um formulário adaptável ou um formulário móvel. O Forms habilitado para sincronização no aplicativo de formulários está disponível na pasta do Forms. Você pode sincronizar formulários ativados no servidor do AEM Forms sem o fluxo de trabalho do AEM Forms (AEM Forms no OSGi).

Consulte:

* [Abrindo uma tarefa](/help/forms/using/open-task.md)
* [Trabalhar com um formulário](/help/forms/using/working-with-form.md)

### Trabalhar offline {#working-offline}

Você pode trabalhar no seu dispositivo móvel no modo offline. Você pode fazer logon no aplicativo mesmo se não houver conectividade de rede e pode trabalhar em todos os formulários que foram sincronizados com o dispositivo quando você estava online pela última vez. Para obter detalhes sobre como sincronizar formulários, consulte [Sincronização do aplicativo](/help/forms/using/sync-app.md). Se você optar por sincronizar os anexos associados a um formulário, também poderá abrir os anexos no modo offline. Você pode editar o formulário, adicionar anotações e enviar ou salvar um formulário no modo offline. O formulário é sincronizado com o servidor do AEM Forms na próxima vez que você estiver online.

Para obter detalhes, consulte [Trabalhar no modo offline](/help/forms/using/work-offline-mode.md).

### Adição de anotações {#adding-annotations}

Você pode adicionar os seguintes anexos a um formulário em seu dispositivo móvel

* **Notas**- Você pode usar o recurso Notas para adicionar um rabisco à mão livre ou uma nota de texto em seu formulário. Para obter detalhes, consulte [Adição de uma observação](/help/forms/using/add-attachments.md#adding-a-note).

* **Imagem**- O aplicativo AEM Forms inclui um recurso que usa a funcionalidade da câmera ou a galeria do dispositivo móvel. Usando o anexo de fotografia, você pode adicionar uma fotografia com o formulário associado. Para obter detalhes, consulte [Adicionar uma fotografia](/help/forms/using/add-attachments.md#adding-a-photograph).

### Salvamento automático {#autosave}

Quando um usuário insere dados no aplicativo AEM Forms, o recurso de salvamento automático os salva em intervalos regulares. O recurso de salvamento automático no aplicativo AEM Forms ajuda a evitar a perda de dados se o aplicativo for fechado devido a condições como bateria fraca.

Consulte [Uso do salvamento automático no aplicativo AEM Forms](/help/forms/using/autosave-data-app.md).

## Diferenças entre a Caixa de entrada do AEM e os recursos do aplicativo AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Duas das principais maneiras de iniciar um fluxo de trabalho centrado no Forms são usar [Caixa de entrada AEM](/help/forms/using/manage-applications-inbox.md) e AEM Forms. No entanto, os recursos da Caixa de entrada AEM e do aplicativo AEM Forms são diferentes. A Caixa de entrada AEM funciona somente com [Fluxos de trabalho centrados na Forms](/help/forms/using/aem-forms-workflow.md) enquanto o aplicativo AEM Forms funciona com fluxos de trabalho e gerenciamento de processos centrados na Forms. Para obter mais informações sobre as diferenças entre os recursos da Caixa de entrada AEM e do aplicativo AEM Forms, consulte [Ações e recursos de fluxos de trabalho do AEM centrados em formulários em fluxos de trabalho OSGi e AEM Forms JEE](capabilities-osgi-jee-workflows.md).

## Formulários suportados {#supported-forms}

Tipos de formulário compatíveis no aplicativo AEM Forms:

### Formulários adaptáveis {#adaptive-form}

Um formulário adaptável que se adapta dinamicamente às entradas do usuário é compatível com o aplicativo AEM Forms. Formulários adaptáveis de carregamento lento também são compatíveis.

### Formulário móvel {#mobile-form}

Você pode criar formulários para dispositivos móveis no AEM Forms. Os formulários móveis são renderizados como formulários HTML em dispositivos móveis que se adaptam de acordo com os dispositivos de exibição.

### Formset {#formset}

Com conjuntos de formulários, vários formulários relacionados a um serviço ou processo podem ser agrupados para automatizar um processo de negócios e apresentados aos usuários finais. Nesse cenário, os usuários podem preencher todo o conjunto como um só e não há necessidade de arquivar, enviar e rastrear formulários ou processos individuais.

>[!NOTE]
>
>Exige fluxo de trabalho do AEM Forms (AEM Forms no JEE).

## Como o aplicativo AEM Forms funciona {#how-aem-forms-app-works}

O aplicativo AEM Forms fornece uma solução móvel para que os funcionários de campo trabalhem em formulários atribuídos a eles. O aplicativo armazena em cache todos os dados do servidor e fornece uma experiência do usuário eficiente, salvando todo o trabalho localmente. Os dados do disco são enviados ao servidor por meio de atualizações de sincronização oportunas.

O aplicativo AEM Forms é um aplicativo baseado no PhoneGap 5.0 no qual o modelo Backbone é usado com eficiência para apresentar dados armazenados nos modelos por meio de exibições. Todas as operações nativas são executadas por meio de plug-ins do PhoneGap.

## Personalizar, criar e distribuir o aplicativo AEM Forms {#customize-build-distribute}

>[!NOTE]
>
>Aplicável somente se estiver usando o código-fonte do aplicativo AEM Forms para criar o aplicativo.

O aplicativo AEM Forms é fácil de personalizar de acordo com as necessidades específicas da organização. O código-fonte do aplicativo é fornecido junto com o AEM Forms. Você pode alterar o código-fonte e criar sua própria solução de força de trabalho móvel. Você também pode assinar o aplicativo com sua própria chave corporativa.

### Personalizar {#customize}

É possível personalizar seu aplicativo para:

**Marcas**: altere o ícone do aplicativo, o nome do aplicativo, as imagens de inicialização e as páginas no aplicativo AEM Forms. Você também pode alterar o texto para localizar o aplicativo em uma região específica. Para obter mais informações sobre a marca do aplicativo AEM Forms, consulte [Personalização da marca](/help/forms/using/branding-customization.md).

**Tema**: altere estilos como cores, fontes e espaçamento na interface do usuário do aplicativo AEM Forms. Para obter mais informações, consulte [Personalização de tema](/help/forms/using/theme-customization.md).

**Gesto**: altere gestos, como deslizar o dedo para a direita e deslizar para a esquerda na interface do usuário do aplicativo AEM Forms. Para obter mais informações, consulte [Personalização de gesto](/help/forms/using/gesture-customization.md).

Para obter mais informações sobre como configurar um projeto de aplicativo do AEM Forms para personalização, consulte:

* [Configurar ambiente para o aplicativo AEM Forms](/help/forms/using/setup-environment-mobile-workspace.md)
* [Configurar projeto do Visual Studio e criar aplicativo do Windows](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Configurar o projeto Xcode e criar o aplicativo iOS](/help/forms/using/setup-xcode-project-build-installer.md)
* [Configurar o projeto Eclipse e criar o aplicativo Android](/help/forms/using/setup-eclipse-project-build-installer.md)

### Criar e distribuir {#build-and-distribute}

O código-fonte do aplicativo AEM Forms pode ser extraído do `adobe-lc-mobileworkspace-src.zip` que está disponível como parte do pacote de origem do aplicativo AEM Forms na Distribuição de software.

Para obter a origem do aplicativo AEM Forms, execute as seguintes etapas:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Selecionar **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. No **[!UICONTROL Filtros]** seção:
   1. Selecionar **[!UICONTROL Forms]** do **[!UICONTROL Solução]** lista suspensa.
   2. Selecione a versão e o tipo do pacote. Você também pode usar a variável **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Selecione o nome do pacote aplicável ao seu sistema operacional e **[!UICONTROL Aceitar termos do EULA]** e selecione **[!UICONTROL Baixar]**.
1. Abertura [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  e clique em **[!UICONTROL Fazer upload do pacote]** para carregar o pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

**Para iOS**:

Para obter detalhes sobre como criar um aplicativo iOS (.ipa), consulte [Configurar o projeto Xcode e criar o aplicativo iOS](/help/forms/using/setup-xcode-project-build-installer.md).

Para obter detalhes sobre como assinar o aplicativo AEM Forms com seu perfil de provisionamento, consulte [Configuração, processo e solução de problemas da assinatura do código do iOS](https://developer.apple.com/support/code-signing/).

**Para Android**:

Para obter detalhes sobre como criar um aplicativo Android (.apk), consulte [Configurar o projeto Eclipse e criar o aplicativo Android](/help/forms/using/setup-eclipse-project-build-installer.md).

Para obter detalhes sobre como assinar o aplicativo AEM Forms, consulte [Assinando seus aplicativos](https://developer.android.com/tools/publishing/app-signing.html).

**Para Windows**:

Para obter detalhes sobre como criar um aplicativo do Windows (.appx), consulte [Configurar o projeto do Visual Studio e criar o aplicativo do Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

Para obter detalhes sobre como distribuir o aplicativo via MDM, consulte [Distribuir o aplicativo AEM Forms](/help/forms/using/distribute-mobile-workspace-app.md). A distribuição de aplicativos via MDM é aplicável somente para iOS e Android.

## Recommendations para atualizar o Espaço de trabalho móvel para o aplicativo AEM Forms {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

Se estiver atualizando para a versão mais recente do aplicativo AEM Forms, leia os seguintes pontos:

* **Se você instalou uma versão anterior do aplicativo da Play Store no Android**
Você pode atualizar o aplicativo diretamente da Play Store.

* **Se uma versão anterior do aplicativo for criada e instalada usando o código-fonte (aplicável para iOS e Android)**:

  Antes de instalar o novo aplicativo, sincronize todos os dados com o servidor do AEM Forms. Depois que os dados forem sincronizados, desinstale a versão anterior do aplicativo e instale o novo aplicativo.
