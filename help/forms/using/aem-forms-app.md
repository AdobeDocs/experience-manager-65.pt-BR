---
title: Aplicativo AEM Forms
seo-title: Aplicativo AEM Forms
description: O aplicativo AEM Forms permite que seus funcionários de campo usem formulários adaptáveis em seus dispositivos móveis.
seo-description: O aplicativo AEM Forms permite que seus funcionários de campo usem formulários adaptáveis em seus dispositivos móveis.
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 0%

---


# Introdução ao aplicativo AEM Forms {#aem-forms-app}

## Visão geral {#overview}

O aplicativo AEM Forms permite a sincronização de formulários adaptáveis, formulários móveis e conjuntos de formulários em dispositivos móveis, com base no seu servidor. Você pode definir workflows que sejam [workflows centrados no Forms em OSGi](/help/forms/using/aem-forms-workflow.md) ou workflows do Forms em JEE. Por exemplo, você gerencia uma empresa bancária e usa a AEM Forms para gerenciar aplicativos e comunicações de clientes. Seus clientes preenchem um formulário e o enviam para verificação. Se você ativar o formulário em dispositivos móveis, seus clientes poderão preenchê-lo no aplicativo AEM Forms. Você também pode gerenciar o fluxo de trabalho de verificação ativando o formulário de verificação em dispositivos móveis. O funcionário de campo pode levar um dispositivo móvel ao cliente, verificar os detalhes e enviar o formulário. O aplicativo AEM Forms sincroniza com o servidor AEM Forms e obtém os formulários ativados para dispositivos móveis. Se o aplicativo estiver offline, ele armazenará dados localmente.

O código-fonte do aplicativo AEM Forms está disponível para os clientes por meio da Distribuição de software. O pacote de código-fonte na Distribuição de software está disponível como: `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

O aplicativo AEM Forms é compatível com dispositivos iOS, Android e Windows. Você pode instalar o aplicativo AEM Forms para Android do Google Play, iOS da App Store e Windows da Windows Store.

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

Para instalar, personalizar e distribuir o aplicativo em dispositivos iOS, Android ou Windows, consulte [Personalizar, criar e distribuir o aplicativo AEM Forms](#customize-build-distribute).

## Pré-requisitos {#prerequisites}

O aplicativo AEM Forms requer um servidor AEM Forms. Os usuários podem renderizar formulários criados no AEM Forms
, preencha-os, salve como rascunhos e envie-os. O aplicativo se conecta ao servidor e obtém formulários ativados dele. O aplicativo AEM Forms sincroniza com o servidor e assim que os formulários são carregados no aplicativo, os usuários podem trabalhar offline. Se o aplicativo estiver offline, os dados serão salvos no dispositivo e os dados serão sincronizados com o servidor quando o aplicativo estiver online.

### Aplicativo AEM Forms com servidores usando AEM Forms Workflow {#aem-forms-app-with-servers-using-aem-forms-workflow}

Se você tiver um servidor AEM Forms Workflow, poderá renderizar formulários como tarefa no aplicativo AEM Forms. Por exemplo, você executa uma empresa bancária e o cliente preenche um aplicativo para usar seus serviços. O aplicativo é um formulário adaptável que aceita informações de seus clientes e as armazena como um envio para revisão. O administrador revê um aplicativo e encaminha uma solicitação de verificação ao funcionário de campo. O aplicativo encaminhado permite um formulário de verificação no aplicativo do trabalhador em campo como uma tarefa. O funcionário de campo leva o dispositivo móvel para o cliente e verifica os detalhes.

### Aplicativo AEM Forms com servidores usando fluxo de trabalho centralizado no Forms no OSGi {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

Se você tiver um servidor AEM Forms, poderá renderizar formulários adaptáveis como AEM aplicativo Caixa de entrada e tarefa no aplicativo AEM Forms. Por exemplo, você executa uma empresa bancária e o cliente preenche um aplicativo para usar seus serviços. O aplicativo está associado a um formulário adaptável que aceita informações de seus clientes e as armazena como um envio para revisão. O administrador revisa a tarefa e aprova a solicitação de verificação para o funcionário de campo. O funcionário de campo leva o dispositivo móvel para o cliente e verifica os detalhes.

### Formulários independentes ou aplicativos AEM Forms com servidores sem o AEM Forms Workflow {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

Um servidor AEM Forms que não usa o AEM Forms Workflow é o AEM Forms no OSGi, um formulário móvel independente ou um formulário adaptável. O aplicativo AEM Forms funciona com sua implementação do AEM Forms em [OSGi](/help/sites-deploying/configuring-osgi.md). O Forms que você habilita e publica para o aplicativo AEM Forms está disponível no aplicativo.

Os formulários são baixados no aplicativo e estão disponíveis offline. Por exemplo, você está executando uma empresa bancária e um cliente preenche um aplicativo em seu site. O aplicativo é um formulário adaptável que aceita informações de seus clientes e as armazena para revisão. O administrador revisa o formulário e cria um formulário de verificação AEM instância do autor. O administrador ativa a sincronização do formulário com o aplicativo AEM Forms e o publica. Se o formulário de verificação estiver disponível no aplicativo AEM Forms, o agente de campo poderá usar um dispositivo móvel para verificar os detalhes do cliente. O dispositivo móvel é sincronizado com o servidor e o formulário de verificação é carregado no aplicativo. Seu agente de campo pode visitar seu cliente, verificar os detalhes, salvar dados como rascunho ou enviar o formulário de verificação. O formulário é sincronizado com o servidor sempre que o aplicativo estiver online.

Para sincronizar seu formulário no aplicativo AEM Forms:

1. Na instância do autor, selecione um formulário e clique em **[!UICONTROL Propriedades da Visualização]**.

1. Na página de propriedades, clique em **[!UICONTROL Avançado]**.
1. Em Avançado, ative a opção: **[!UICONTROL Sincronize com o aplicativo AEM Forms]** e toque em **[!UICONTROL Salvar]**.

Quando o formulário é publicado, o aplicativo é sincronizado com o servidor e busca o formulário. Para sincronizar vários formulários, na instância do autor, selecione vários formulários no gerenciador de formulários e toque em **[!UICONTROL Sincronizar com o AEM Forms App]**.

## Suporte a dispositivos móveis {#mobile-device-support}

Consulte [Aplicativo AEM Forms (anteriormente conhecido como Mobile Workspace)](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## Principais recursos do aplicativo AEM Forms {#key-features-of-aem-forms-app}

### Aplicativo AEM Forms com servidores AEM Forms {#aem-forms-app-with-aem-forms-servers}

Você pode sincronizar seu aplicativo com o servidor AEM Forms e trabalhar com formulários em seu dispositivo móvel.

Com o servidor do AEM Forms Workflow, um formulário pode ser associado a um ponto de partida em um processo de análise de big data e AEM aplicativo Caixa de entrada. Um aplicativo AEM Caixa de entrada pode ter um formulário adaptável associado a ele. Um ponto de partida pode ter um formulário adaptável, um formulário HTML5 ou um conjunto de formulários associado a ele. Um ponto de partida pode ser enviado como uma tarefa ou a tarefa pode ser salva como um rascunho. Para obter mais informações sobre as diferenças entre um aplicativo AEM Caixa de entrada e um ponto de partida, consulte [Ações e recursos de Workflows AEM centrados em formulários em workflows OSGi e AEM Forms JEE](capabilities-osgi-jee-workflows.md).

Com o servidor AEM Forms sem fluxo de trabalho AEM Forms, um formulário habilitado para sincronização no aplicativo é renderizado no aplicativo AEM Forms. A Forms está disponível na guia Forms do aplicativo, pode ser enviada ou salva como rascunho. Formulários adaptáveis e móveis são suportados no aplicativo.

1. **Salvar uma tarefa ou formulário como rascunho**

   A opção salvar como rascunho salva um instantâneo de uma tarefa ou formulário juntamente com os dados preenchidos e os arquivos anexados no formulário associado. Os rascunhos são salvos no dispositivo móvel e sincronizados com o servidor AEM Forms para uma recuperação posterior.

   Consulte [Salvar uma tarefa ou formulário como um rascunho](/help/forms/using/save-as-draft.md).

1. **Salvar formulário como modelo**

   Às vezes, quando os usuários preenchem um formulário, as entradas em alguns campos permanecem as mesmas. Para essas instâncias, é possível preencher os campos que exigem valores idênticos em cada instância e salvar o formulário ou rascunho como modelo. Agora, toda vez que você cria uma instância do modelo, os campos especificados já são preenchidos com valores especificados no modelo. Ajuda a economizar tempo e esforço necessários para preencher o formulário.

   Consulte [Salvar formulários como modelos](/help/forms/using/save-forms-and-start-points-as-templates.md).

### Trabalhar com tarefas e formulários {#working-with-tasks-and-forms}

Você pode sincronizar seu aplicativo com o servidor do AEM Forms Workflow e trabalhar com tarefa e formulários no dispositivo móvel.

Uma tarefa no dispositivo móvel contém um formulário adaptável, um formulário HTML5 ou um conjunto de formulários e também pode conter anexos e [URL de resumo](/help/forms/using/getting-task-variables-summary-url.md). Por padrão, as tarefas atribuídas a você são colocadas na pasta **[!UICONTROL Tarefa]**. Ao trabalhar em uma tarefa, você pode alterar a tarefa e salvar uma cópia de rascunho da tarefa no servidor AEM Forms.

Um formulário no dispositivo móvel pode ser um formulário adaptável ou um formulário móvel. O Forms ativado para sincronização no aplicativo de formulários está disponível na pasta Forms. É possível sincronizar formulários ativados no servidor AEM Forms sem fluxo de trabalho do AEM Forms (AEM Forms no OSGi).

Consulte:

* [Abrir uma tarefa](/help/forms/using/open-task.md)
* [Como trabalhar com um formulário](/help/forms/using/working-with-form.md)

### Trabalhando offline {#working-offline}

Você pode trabalhar em seu dispositivo móvel no modo offline. Você pode fazer logon no aplicativo mesmo se não houver conectividade de rede e funcionar em todos os formulários que foram sincronizados com o dispositivo na última vez que você estava online. Para obter detalhes sobre como sincronizar seus formulários, consulte [Sincronizar o aplicativo](/help/forms/using/sync-app.md). Se você optar por sincronizar os anexos associados a um formulário, também poderá abrir os anexos no modo offline. É possível editar o formulário, adicionar anotações e enviar ou salvar um formulário no modo offline. O formulário será sincronizado com o servidor AEM Forms na próxima vez que você estiver on-line.

Para obter detalhes, consulte [Trabalhando no modo offline](/help/forms/using/work-offline-mode.md).

### Adicionar anotações {#adding-annotations}

É possível adicionar os seguintes anexos a um formulário no dispositivo móvel

* **Notas** - Você pode usar o recurso Anotações para adicionar um script à mão livre ou uma nota de texto no formulário. Para obter detalhes, consulte [Adicionar uma nota](/help/forms/using/add-attachments.md#adding-a-note).

* **Imagem** - O aplicativo AEM Forms inclui um recurso que usa a funcionalidade da câmera ou a galeria do seu dispositivo móvel. Usando o anexo de fotografia, você pode adicionar uma fotografia com o formulário associado. Para obter detalhes, consulte [Adicionar uma fotografia](/help/forms/using/add-attachments.md#adding-a-photograph).

### Salvar automaticamente {#autosave}

Quando um usuário digita dados no aplicativo AEM Forms, o recurso de gravação automática os salva em intervalos regulares. O recurso de gravação automática no aplicativo AEM Forms ajuda a evitar perda de dados se o aplicativo for fechado devido a condições como bateria fraca.

Consulte [Uso do salvamento automático em aplicativos AEM Forms](/help/forms/using/autosave-data-app.md).

## Diferenças entre AEM Caixa de entrada e os recursos do aplicativo AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Duas das principais maneiras de iniciar um fluxo de trabalho centrado na Forms estão usando [AEM Caixa de entrada](/help/forms/using/manage-applications-inbox.md) e aplicativos AEM Forms. No entanto, os recursos de AEM Caixa de entrada e aplicativos AEM Forms são diferentes. AEM Caixa de entrada funciona somente com [workflows centrados no Forms](/help/forms/using/aem-forms-workflow.md) enquanto o aplicativo AEM Forms funciona com workflows centrados no Forms e com gerenciamento de processos. Para obter mais informações sobre as diferenças entre AEM Caixa de entrada e os recursos do aplicativo AEM Forms, consulte [Ações e recursos de Workflows AEM centrados em formulários em OSGi e workflows AEM Forms JEE](capabilities-osgi-jee-workflows.md).

## Formulários suportados {#supported-forms}

Tipos de formulário suportados no aplicativo AEM Forms:

### Formulários adaptáveis {#adaptive-form}

Um formulário adaptável que se adapta dinamicamente às entradas do usuário é suportado no aplicativo AEM Forms. Formulários adaptativos com carga lenta também são suportados.

### Formulário móvel {#mobile-form}

Você pode criar formulários para dispositivos móveis no AEM Forms. Formulários móveis são renderizados como formulários HTML em dispositivos móveis que se adaptam de acordo com dispositivos de exibição.

### Formset {#formset}

Com conjuntos de formulários, vários formulários relacionados a um serviço ou processo podem ser agrupados para automatizar um processo de negócios e apresentados aos usuários finais. Nesse cenário, os usuários podem preencher o conjunto inteiro como um único e não há necessidade de arquivar, enviar e rastrear formulários ou processos individuais.

>[!NOTE]
>
>Requer AEM Forms Workflow (AEM Forms em JEE).

## Como o aplicativo AEM Forms funciona {#how-aem-forms-app-works}

O aplicativo AEM Forms fornece uma solução móvel para que trabalhadores de campo trabalhem em formulários atribuídos a eles. O aplicativo armazena em cache os dados completos do servidor e fornece uma experiência de usuário eficiente ao salvar todo o trabalho localmente. Os dados do disco são enviados para o servidor por meio de atualizações de sincronização oportunas.

O aplicativo AEM Forms é um aplicativo baseado no PhoneGap 5.0 no qual o modelo Backbone é usado eficientemente para apresentar dados armazenados nos modelos por meio do visualização. Todas as operações nativas são executadas por meio de plug-ins PhoneGap.

## Personalize, crie e distribua o aplicativo AEM Forms {#customize-build-distribute}

>[!NOTE]
>
>Aplicável somente se você estiver usando o código fonte do aplicativo AEM Forms para criar o aplicativo.

O aplicativo AEM Forms é fácil de personalizar para necessidades específicas da organização. O código fonte do aplicativo é fornecido junto com a AEM Forms. Você pode alterar o código fonte e criar sua própria solução de força de trabalho móvel. Você também pode assinar o aplicativo com sua própria chave corporativa.

### Personalizar {#customize}

Você pode personalizar seu aplicativo para:

**Marca**: Altere o ícone do aplicativo, o nome do aplicativo, as imagens de inicialização e as páginas no aplicativo AEM Forms. Você também pode alterar o texto para localizar o aplicativo para uma região específica. Para obter mais informações sobre a marca do aplicativo AEM Forms, consulte [Personalização da marca](/help/forms/using/branding-customization.md).

**Tema**: Altere estilos como cores, fontes e espaçamento na interface do usuário do aplicativo AEM Forms. Para obter mais informações, consulte [Personalização do tema](/help/forms/using/theme-customization.md).

**Gesto**: Altere gestos, como deslizar para a direita e deslizar para a esquerda na interface do usuário do aplicativo AEM Forms. Para obter mais informações, consulte [Personalização do gesto](/help/forms/using/gesture-customization.md).

Para obter mais informações sobre como configurar um projeto de aplicativo AEM Forms para personalização, consulte:

* [Configurar ambiente para aplicativos AEM Forms](/help/forms/using/setup-environment-mobile-workspace.md)
* [Configurar projeto do Visual Studio e criar aplicativo do Windows](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Configurar projeto Xcode e criar aplicativo iOS](/help/forms/using/setup-xcode-project-build-installer.md)
* [Configurar projeto do Eclipse e criar aplicativo Android](/help/forms/using/setup-eclipse-project-build-installer.md)

### Criar e distribuir {#build-and-distribute}

O código fonte do aplicativo AEM Forms pode ser extraído do `adobe-lc-mobileworkspace-src.zip` que está disponível como parte do pacote de origem do aplicativo AEM Forms na Distribuição de software.

Para obter a fonte do aplicativo AEM Forms, execute as seguintes etapas:

1. Abra [Distribuição de software](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Software Distribution (Distribuição de software).
1. Toque em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. Na seção **[!UICONTROL Filtros]**:
   1. Selecione **[!UICONTROL Forms]** na lista suspensa **[!UICONTROL Solution]**.
   2. Selecione a versão e o tipo do pacote. Você também pode usar a opção **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Toque no nome do pacote aplicável ao seu sistema operacional, selecione **[!UICONTROL Aceitar termos do EULA]** e toque em **[!UICONTROL Download]**.
1. Abra [Gerenciador de pacotes](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) e clique em **[!UICONTROL Carregar pacote]** para fazer upload do pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

**Para iOS**:

Para obter detalhes sobre como criar um aplicativo iOS (.ipa), consulte [Configure o projeto Xcode e crie o aplicativo iOS](/help/forms/using/setup-xcode-project-build-installer.md).

Para obter detalhes sobre como assinar o aplicativo AEM Forms com seu perfil de provisionamento, consulte [Configuração, processo e solução de problemas de assinatura de código iOS](https://developer.apple.com/support/code-signing/).

**Para Android**:

Para obter detalhes sobre como criar um aplicativo Android (.apk), consulte [Configure o projeto Eclipse e crie o aplicativo Android](/help/forms/using/setup-eclipse-project-build-installer.md).

Para obter detalhes sobre como assinar o aplicativo AEM Forms, consulte [Assinando seus aplicativos](https://developer.android.com/tools/publishing/app-signing.html).

**Para Windows**:

Para obter detalhes sobre como criar um aplicativo do Windows (.appx), consulte [Configure o projeto do Visual Studio e crie o aplicativo do Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

Para obter detalhes sobre como distribuir o aplicativo via MDM, consulte [Distribuir aplicativo AEM Forms](/help/forms/using/distribute-mobile-workspace-app.md). A distribuição de aplicativos por meio do MDM é aplicável somente para iOS e Android.

## Recommendations para atualizar o Mobile Workspace para o aplicativo AEM Forms {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

Se você estiver atualizando para a versão mais recente do aplicativo AEM Forms, certifique-se de ler os seguintes pontos:

* **Se você instalou uma versão anterior do aplicativo da loja de reprodução no**
Android, é possível atualizar o aplicativo diretamente da loja de reprodução.

* **Se a versão anterior do aplicativo for criada e instalada usando o código fonte (aplicável para iOS e Android)**:

   Antes de instalar o novo aplicativo, sincronize todos os seus dados com o servidor AEM Forms. Depois que os dados forem sincronizados, desinstale a versão anterior do aplicativo e instale o novo aplicativo.

