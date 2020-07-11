---
title: aplicativo AEM Forms
seo-title: aplicativo AEM Forms
description: O aplicativo AEM Forms permite que seus trabalhadores de campo usem formulários adaptáveis em seus dispositivos móveis.
seo-description: O aplicativo AEM Forms permite que seus trabalhadores de campo usem formulários adaptáveis em seus dispositivos móveis.
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 0%

---


# Introduction to AEM Forms app {#aem-forms-app}

## Visão geral {#overview}

O aplicativo AEM Forms permite a sincronização de formulários adaptáveis, formulários móveis e conjuntos de formulários em dispositivos móveis, com base no seu servidor. É possível definir workflows que são workflows centrados no [Forms em OSGi](/help/forms/using/aem-forms-workflow.md) ou workflows [do Forms em JEE](/help/forms/using/finance-reference-site-walkthrough.md#approving-the-application). Por exemplo, você gerencia uma empresa bancária e usa AEM Forms para gerenciar aplicativos e comunicações de clientes. Seus clientes preenchem um formulário e o enviam para verificação. Se você ativar o formulário em dispositivos móveis, seus clientes poderão preenchê-lo no aplicativo AEM Forms. Você também pode gerenciar o fluxo de trabalho de verificação ativando o formulário de verificação em dispositivos móveis. O funcionário de campo pode levar um dispositivo móvel ao cliente, verificar os detalhes e enviar o formulário. O aplicativo AEM Forms sincroniza com o servidor AEM Forms e obtém os formulários ativados para dispositivos móveis. Se o aplicativo estiver offline, ele armazenará dados localmente.

O código-fonte do aplicativo AEM Forms está disponível para os clientes por meio da Distribuição de software. O pacote de código-fonte na Distribuição de software está disponível como: `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

O aplicativo AEM Forms é compatível com dispositivos iOS, Android e Windows. Você pode instalar o aplicativo AEM Forms para Android do Google Play, iOS da App Store e Windows da Windows Store do Windows.

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

Para instalar, personalizar e distribuir o aplicativo em dispositivos iOS, Android ou Windows, consulte [Personalizar, criar e distribuir o aplicativo](#customize-build-distribute)AEM Forms.

## Pré-requisitos {#prerequisites}

O aplicativo AEM Forms requer um servidor AEM Forms. Os usuários podem renderizar formulários criados no servidor do AEM Forms, preenchê-los, salvar como rascunhos e enviá-los. O aplicativo se conecta ao servidor e obtém formulários ativados dele. O aplicativo AEM Forms sincroniza com o servidor e assim que os formulários são carregados no aplicativo, os usuários podem trabalhar offline. Se o aplicativo estiver offline, os dados serão salvos no dispositivo e os dados serão sincronizados com o servidor quando o aplicativo estiver online.

### AEM Forms o aplicativo com servidores usando o Fluxo de trabalho do AEM Forms {#aem-forms-app-with-servers-using-aem-forms-workflow}

Se você tiver um servidor de Fluxo de trabalho do AEM Forms, poderá renderizar formulários como tarefas no aplicativo AEM Forms. Por exemplo, você executa uma empresa bancária e o cliente preenche um aplicativo para usar seus serviços. O aplicativo é um formulário adaptável que aceita informações de seus clientes e as armazena como um envio para revisão. O administrador revê um aplicativo e encaminha uma solicitação de verificação ao funcionário de campo. O aplicativo encaminhado permite um formulário de verificação no aplicativo do trabalhador em campo como uma tarefa. O funcionário de campo leva o dispositivo móvel para o cliente e verifica os detalhes.

### Aplicativo AEM Forms com servidores usando fluxo de trabalho centralizado em formulários no OSGi {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

Se você tiver um servidor AEM Forms, poderá renderizar formulários adaptáveis como aplicativos AEM Inbox e tarefa no aplicativo AEM Forms. Por exemplo, você executa uma empresa bancária e o cliente preenche um aplicativo para usar seus serviços. O aplicativo está associado a um formulário adaptável que aceita informações de seus clientes e as armazena como um envio para revisão. O administrador revisa a tarefa e aprova a solicitação de verificação para o funcionário de campo. O funcionário de campo leva o dispositivo móvel para o cliente e verifica os detalhes.

### Aplicativos de formulários ou AEM Forms independentes com servidores sem fluxo de trabalho do AEM Forms {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

Um servidor AEM Forms que não usa o Fluxo de trabalho de AEM Forms é um AEM Forms no OSGi ou um formulário móvel independente ou um formulário adaptável. O aplicativo AEM Forms funciona com sua implementação de AEM Forms no [OSGi](/help/sites-deploying/configuring-osgi.md). Os formulários que você ativa e publica para o aplicativo AEM Forms estão disponíveis no aplicativo.

Os formulários são baixados no aplicativo e estão disponíveis offline. Por exemplo, você está executando uma empresa bancária e um cliente preenche um aplicativo em seu site. O aplicativo é um formulário adaptável que aceita informações de seus clientes e as armazena para revisão. O administrador revisa o formulário e cria um formulário de verificação na instância do autor de AEM. O administrador ativa a sincronização do formulário com o aplicativo AEM Forms e o publica. Se o formulário de verificação estiver disponível no aplicativo AEM Forms, o agente de campo poderá usar um dispositivo móvel para verificar os detalhes do cliente. O dispositivo móvel é sincronizado com o servidor e o formulário de verificação é carregado no aplicativo. Seu agente de campo pode visitar seu cliente, verificar os detalhes, salvar dados como rascunho ou enviar o formulário de verificação. O formulário é sincronizado com o servidor sempre que o aplicativo estiver online.

Para sincronizar seu formulário no aplicativo AEM Forms:

1. Na instância do autor, selecione um formulário e clique em Propriedades **[!UICONTROL da]** Visualização.

1. Na página de propriedades, clique em **[!UICONTROL Avançado]**.
1. Em Avançado, ative a opção: **[!UICONTROL Sincronize com o aplicativo]** AEM Forms e toque em **[!UICONTROL Salvar]**.

Quando o formulário é publicado, o aplicativo é sincronizado com o servidor e busca o formulário. Para sincronizar vários formulários, na instância do autor, selecione vários formulários no gerenciador de formulários e toque em **[!UICONTROL Sincronizar com o aplicativo]** AEM Forms.

## Suporte para dispositivos móveis {#mobile-device-support}

Consulte Aplicativo [AEM Forms (anteriormente conhecido como Mobile Workspace)](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## Principais recursos do aplicativo AEM Forms {#key-features-of-aem-forms-app}

### Aplicativo AEM Forms com servidores AEM Forms {#aem-forms-app-with-aem-forms-servers}

Você pode sincronizar seu aplicativo com o servidor AEM Forms e trabalhar com formulários em seu dispositivo móvel.

Com o servidor de Fluxo de trabalho do AEM Forms, um formulário pode ser associado a um ponto de partida em um processo de análise de big data e ao aplicativo de Caixa de entrada do AEM. Um aplicativo AEM Inbox pode ter um formulário adaptável associado a ele. Um ponto de partida pode ter um formulário adaptável, um formulário HTML5 ou um conjunto de formulários associado a ele. Um ponto de partida pode ser enviado como uma tarefa ou a tarefa pode ser salva como um rascunho. Para obter mais informações sobre as diferenças entre um aplicativo AEM Inbox e um ponto de partida, consulte [Ações e recursos de Workflows AEM centrados em forma em workflows](capabilities-osgi-jee-workflows.md)OSGi e AEM Forms JEE.

Com o servidor AEM Forms sem fluxo de trabalho de AEM Forms, um formulário habilitado para sincronização no aplicativo é renderizado no aplicativo AEM Forms. Os formulários estão disponíveis na guia Formulários do aplicativo, podem ser enviados ou salvos como rascunho. Formulários adaptáveis e móveis são suportados no aplicativo.

1. **Salvar uma tarefa ou formulário como rascunho**

   A opção salvar como rascunho salva um instantâneo de uma tarefa ou formulário juntamente com os dados preenchidos e os arquivos anexados no formulário associado. Os rascunhos são salvos no dispositivo móvel e sincronizados com o servidor AEM Forms para uma recuperação posterior.

   Consulte [Salvar uma tarefa ou formulário como rascunho](/help/forms/using/save-as-draft.md).

1. **Salvar formulário como modelo**

   Às vezes, quando os usuários preenchem um formulário, as entradas em alguns campos permanecem as mesmas. Para essas instâncias, é possível preencher os campos que exigem valores idênticos em cada instância e salvar o formulário ou rascunho como modelo. Agora, toda vez que você cria uma instância do modelo, os campos especificados já são preenchidos com valores especificados no modelo. Ajuda a economizar tempo e esforço necessários para preencher o formulário.

   Consulte [Salvar formulários como modelos](/help/forms/using/save-forms-and-start-points-as-templates.md).

### Trabalhar com tarefas e formulários {#working-with-tasks-and-forms}

Você pode sincronizar seu aplicativo com o servidor de Fluxo de trabalho do AEM Forms e trabalhar com tarefa e formulários em seu dispositivo móvel.

Uma tarefa no dispositivo móvel contém um formulário adaptável, um formulário HTML5 ou um conjunto de formulários e também pode conter anexos e URL [de](/help/forms/using/getting-task-variables-summary-url.md)resumo. Por padrão, as tarefas atribuídas a você são colocadas na pasta **[!UICONTROL Tarefa]** . Ao trabalhar em uma tarefa, você pode alterar a tarefa e salvar uma cópia de rascunho da tarefa no servidor AEM Forms.

Um formulário no dispositivo móvel pode ser um formulário adaptável ou um formulário móvel. Os formulários ativados para sincronização no aplicativo de formulários estão disponíveis na pasta Formulários. É possível sincronizar formulários ativados no servidor AEM Forms sem fluxo de trabalho do AEM Forms (AEM Forms no OSGi).

Consulte:

* [Abrir uma tarefa](/help/forms/using/open-task.md)
* [Como trabalhar com um formulário](/help/forms/using/working-with-form.md)

### Trabalhar offline {#working-offline}

Você pode trabalhar em seu dispositivo móvel no modo offline. Você pode fazer logon no aplicativo mesmo se não houver conectividade de rede e funcionar em todos os formulários que foram sincronizados com o dispositivo na última vez que você estava online. Para obter detalhes sobre como sincronizar formulários, consulte [Sincronizar o aplicativo](/help/forms/using/sync-app.md). Se você optar por sincronizar os anexos associados a um formulário, também poderá abrir os anexos no modo offline. É possível editar o formulário, adicionar anotações e enviar ou salvar um formulário no modo offline. O formulário será sincronizado com o servidor AEM Forms na próxima vez que você estiver on-line.

Para obter detalhes, consulte [Trabalho no modo](/help/forms/using/work-offline-mode.md)offline.

### Adding annotations {#adding-annotations}

É possível adicionar os seguintes anexos a um formulário no dispositivo móvel

* **Notas**- Você pode usar o recurso Anotações para adicionar um script à mão livre ou uma nota de texto no formulário. Para obter detalhes, consulte [Adicionar uma nota](/help/forms/using/add-attachments.md#adding-a-note).

* **Imagem**: o aplicativo AEM Forms inclui um recurso que usa a funcionalidade da câmera ou a galeria do seu dispositivo móvel. Usando o anexo de fotografia, você pode adicionar uma fotografia com o formulário associado. Para obter detalhes, consulte [Adicionar uma fotografia](/help/forms/using/add-attachments.md#adding-a-photograph).

### Salvamento automático {#autosave}

Quando um usuário digita dados no aplicativo AEM Forms, o recurso de salvamento automático os salva em intervalos regulares. O recurso de gravação automática no aplicativo AEM Forms ajuda a evitar perda de dados se o aplicativo for fechado devido a condições como bateria fraca.

Consulte [Uso do salvamento automático em aplicativos](/help/forms/using/autosave-data-app.md)AEM Forms.

## Diferenças entre os recursos da Caixa de entrada do AEM e do aplicativo AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Duas das principais maneiras de iniciar um fluxo de trabalho centrado no Forms são usar o aplicativo [AEM Inbox](/help/forms/using/manage-applications-inbox.md) e o aplicativo AEM Forms. Os recursos da Caixa de entrada do AEM e do aplicativo AEM Forms, no entanto, são diferentes. A Caixa de entrada do AEM funciona somente com workflows [centrados no](/help/forms/using/aem-forms-workflow.md) Forms, enquanto o aplicativo AEM Forms funciona com workflows centrados no Forms e também com gerenciamento de processos. Para obter mais informações sobre as diferenças entre os recursos da Caixa de entrada do AEM e do aplicativo AEM Forms, consulte [Ações e recursos de Workflows AEM centrados em forma em workflows](capabilities-osgi-jee-workflows.md)JEE OSGi e AEM Forms.

## Formulários suportados {#supported-forms}

Tipos de formulário suportados no aplicativo AEM Forms:

### Formulários adaptáveis {#adaptive-form}

Um formulário adaptável que se adapta dinamicamente às entradas do usuário é suportado no aplicativo AEM Forms. Formulários adaptativos com carga lenta também são suportados.

### Formulário móvel {#mobile-form}

É possível criar formulários para dispositivos móveis no AEM Forms. Formulários móveis são renderizados como formulários HTML em dispositivos móveis que se adaptam de acordo com dispositivos de exibição.

### Formset {#formset}

Com conjuntos de formulários, vários formulários relacionados a um serviço ou processo podem ser agrupados para automatizar um processo de negócios e apresentados aos usuários finais. Nesse cenário, os usuários podem preencher o conjunto inteiro como um único e não há necessidade de arquivar, enviar e rastrear formulários ou processos individuais.

>[!NOTE]
>
>Requer fluxo de trabalho de AEM Forms (AEM Forms no JEE).

## Como o aplicativo AEM Forms funciona {#how-aem-forms-app-works}

O aplicativo AEM Forms fornece uma solução móvel para que os trabalhadores de campo trabalhem em formulários atribuídos a eles. O aplicativo armazena em cache os dados completos do servidor e fornece uma experiência de usuário eficiente ao salvar todo o trabalho localmente. Os dados do disco são enviados para o servidor por meio de atualizações de sincronização oportunas.

O aplicativo AEM Forms é um aplicativo baseado no PhoneGap 5.0 no qual o modelo Backbone é usado com eficiência para apresentar dados armazenados nos modelos por meio do visualização. Todas as operações nativas são executadas por meio de plug-ins PhoneGap.

## Personalize, crie e distribua o aplicativo AEM Forms {#customize-build-distribute}

>[!NOTE]
>
>Aplicável somente se você estiver usando o código fonte do aplicativo AEM Forms para criar o aplicativo.

O aplicativo AEM Forms é fácil de personalizar para necessidades específicas da organização. O código fonte do aplicativo é fornecido junto com AEM Forms. Você pode alterar o código fonte e criar sua própria solução de força de trabalho móvel. Você também pode assinar o aplicativo com sua própria chave corporativa.

### Personalizar {#customize}

Você pode personalizar seu aplicativo para:

**Marca**: Altere o ícone do aplicativo, o nome do aplicativo, as imagens de ativação e as páginas no aplicativo AEM Forms. Você também pode alterar o texto para localizar o aplicativo para uma região específica. Para obter mais informações sobre a marca do aplicativo AEM Forms, consulte Personalização [da](/help/forms/using/branding-customization.md)marca.

**Tema**: Altere estilos como cores, fontes e espaçamento na interface do usuário do aplicativo AEM Forms. Para obter mais informações, consulte Personalização [do tema](/help/forms/using/theme-customization.md).

**Gesto**: Altere gestos, como deslizar para a direita e deslizar para a esquerda na interface do usuário do aplicativo AEM Forms. Para obter mais informações, consulte Personalização [do gesto](/help/forms/using/gesture-customization.md).

Para obter mais informações sobre como configurar um projeto de aplicativo AEM Forms para personalização, consulte:

* [Configurar ambiente para aplicativo AEM Forms](/help/forms/using/setup-environment-mobile-workspace.md)
* [Configurar projeto do Visual Studio e criar aplicativo do Windows](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Configurar projeto Xcode e criar aplicativo iOS](/help/forms/using/setup-xcode-project-build-installer.md)
* [Configurar projeto do Eclipse e criar aplicativo Android](/help/forms/using/setup-eclipse-project-build-installer.md)

### Criar e distribuir {#build-and-distribute}

O código fonte do aplicativo AEM Forms pode ser extraído do `adobe-lc-mobileworkspace-src.zip` que está disponível como parte do pacote de origem do aplicativo AEM Forms na Distribuição de software.

Para obter a fonte do aplicativo AEM Forms, execute as seguintes etapas:

1. Distribuição [de](https://experience.adobe.com/downloads)software aberta. Você precisa de um Adobe ID para fazer login na Software Distribution (Distribuição de software).
1. Toque em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. Na seção **[!UICONTROL Filtros]** :
   1. Selecione **[!UICONTROL Formulários]** na lista suspensa **[!UICONTROL Solução]** .
   2. Selecione a versão e o tipo do pacote. Você também pode usar a opção **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Toque no nome do pacote aplicável ao seu sistema operacional, selecione **[!UICONTROL Aceitar termos]** do EULA e toque em **[!UICONTROL Download]**.
1. Abra o Gerenciador [de](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) pacotes e clique em **[!UICONTROL Carregar pacote]** para fazer upload do pacote.
1. Select the package and click **[!UICONTROL Install]**.

**Para iOS**:

Para obter detalhes sobre como criar um aplicativo iOS (.ipa), consulte [Configurar o projeto Xcode e criar o aplicativo](/help/forms/using/setup-xcode-project-build-installer.md)iOS.

Para obter detalhes sobre como assinar o aplicativo AEM Forms com seu perfil de provisionamento, consulte Configuração, processo e solução de problemas [de assinatura de código](https://developer.apple.com/support/code-signing/)iOS.

**Para Android**:

Para obter detalhes sobre como criar um aplicativo Android (.apk), consulte [Configurar o projeto Eclipse e criar o aplicativo](/help/forms/using/setup-eclipse-project-build-installer.md)Android.

Para obter detalhes sobre como assinar o aplicativo AEM Forms, consulte [Assinando seus aplicativos](https://developer.android.com/tools/publishing/app-signing.html).

**Para Windows**:

Para obter detalhes sobre como criar um aplicativo do Windows (.appx), consulte [Configurar o projeto do Visual Studio e criar o aplicativo](/help/forms/using/setup-visual-studio-project-build-installer.md)do Windows.

Para obter detalhes sobre como distribuir o aplicativo via MDM, consulte [Distribute AEM Forms app](/help/forms/using/distribute-mobile-workspace-app.md). A distribuição de aplicativos por meio do MDM é aplicável somente para iOS e Android.

## Recomendações para atualizar o Mobile Workspace para o aplicativo AEM Forms {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

Se você estiver atualizando para a versão mais recente do aplicativo AEM Forms, certifique-se de ler os seguintes pontos:

* **Se você instalou uma versão anterior do aplicativo da loja de reprodução no Android** Você pode atualizar o aplicativo diretamente da loja de reprodução.

* **Se a versão anterior do aplicativo for criada e instalada usando o código fonte (aplicável para iOS e Android)**:

   Antes de instalar o novo aplicativo, sincronize todos os seus dados com o servidor AEM Forms. Depois que os dados forem sincronizados, desinstale a versão anterior do aplicativo e instale o novo aplicativo.

