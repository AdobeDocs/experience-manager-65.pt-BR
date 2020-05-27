---
title: Integração com o Adobe Campaign Standard
seo-title: Integração com o Adobe Campaign Standard
description: Integração com o Adobe Campaign Standard.
seo-description: Integração com o Adobe Campaign Standard.
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
translation-type: tm+mt
source-git-commit: f951c195c581f770dcc87fdf4a89d40ee6dd9ec0
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 0%

---


# Integração com o Adobe Campaign Standard{#integrating-with-adobe-campaign-standard}

>[!NOTE]
>
>Esta documentação descreve como integrar o AEM ao Adobe Campaign Standard, a solução baseada em subscrições. Se estiver usando o Adobe Campaign 6.1, consulte [Integração com o Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md) para obter essas instruções.

O Adobe Campaign permite gerenciar o conteúdo e os formulários de delivery de email diretamente no Adobe Experience Manager.

Para usar as duas soluções juntas ao mesmo tempo, primeiro configure-as para se conectarem umas às outras. Isso envolve etapas de configuração no Adobe Campaign e no Adobe Experience Manager. Essas etapas são descritas detalhadamente neste documento.

Trabalhar com o Adobe Campaign no AEM inclui a capacidade de enviar emails e formulários por meio do Adobe Campaign e está descrita em [Trabalhar com o Adobe Campaign](/help/sites-authoring/campaign.md).

Além disso, os seguintes tópicos podem ser de interesse ao integrar o AEM ao [Adobe Campaign](https://docs.campaign.adobe.com/doc/standard/en/home.html):

* [Práticas recomendadas para modelos de e-mail](/help/sites-administering/best-practices-for-email-templates.md)
* [Solução de problemas de integração com seu Adobe Campaign](/help/sites-administering/troubleshooting-campaignintegration.md)

Se você estiver estendendo sua integração com o Adobe Campaign, talvez deseje ver as seguintes páginas:

* [Criação de extensões personalizadas](/help/sites-developing/extending-campaign-extensions.md)
* [Criação de mapeamentos de formulário personalizados](/help/sites-developing/extending-campaign-form-mapping.md)

## Configurando o Adobe Campaign {#configuring-adobe-campaign}

A configuração do Adobe Campaign envolve o seguinte:

1. Configuração do usuário **aemserver** .
1. Criando uma conta externa dedicada.
1. Verificação da opção AEMResourceTypeFilter.
1. Criando um template do delivery dedicado.

>[!NOTE]
>
>Para executar essas operações, é necessário ter a função de **administração** no Adobe Campaign.

### Pré-requisitos {#prerequisites}

Verifique se você tem os seguintes elementos antecipadamente:

* [Uma instância de criação do AEM](/help/sites-deploying/deploy.md#getting-started)
* [Uma instância de publicação do AEM](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Uma instância Adobe Campaign](https://docs.adobe.com/content/docs/en/campaign/ACS.html)

>[!CAUTION]
>
>As operações detalhadas nas seções [Configuração do Adobe Campaign](#configuring-adobe-campaign) e [Configuração do Adobe Experience Manager](#configuring-adobe-experience-manager) são necessárias para que as funcionalidades de integração entre o AEM e o Adobe Campaign funcionem corretamente.

### Configuração do usuário aemserver {#configuring-the-aemserver-user}

O usuário **aemserver** deve estar configurado no Adobe Campaign. O **aemserver** é um usuário técnico que será usado para conectar o servidor AEM ao Adobe Campaign.

Vá até **Administração** > **Usuários e segurança** > **Usuários** e selecione o usuário **aemserver** . Clique nele para abrir as configurações do usuário.

* É necessário definir uma senha para este usuário. Isso não pode ser feito por meio da interface do usuário. Essa configuração deve ser feita em REST por um administrador técnico.
* Você pode atribuir funções específicas a esse usuário, como **deliveryPrepare**, que permite que o usuário crie e edite delivery.

### Configuração de uma conta externa do Adobe Experience Manager {#configuring-an-adobe-experience-manager-external-account}

Você deve configurar uma conta externa que permita conectar o Adobe Campaign à sua instância do AEM.

>[!NOTE]
>
>No AEM, certifique-se de definir a senha para o usuário remoto de campanha. É necessário definir essa senha para conectar o Adobe Campaign ao AEM. Faça logon como administrador e no console de administração do usuário, procure o usuário remoto-campanha e clique em **Definir senha**.

Para configurar uma conta externa do AEM:

1. Vá até **Administração** > Configurações **** do aplicativo > **Conta externa**.

   ![chlimage_1-124](assets/chlimage_1-124a.png)

1. Selecione a conta externa **aemInstance** padrão ou crie uma nova clicando no botão **Criar** .
1. Selecione **Adobe Experience** Manager no campo **Tipo** e insira os parâmetros de acesso usados para sua instância de criação do AEM: endereço do servidor, nome da conta e senha.

   >[!NOTE]
   >
   >Certifique-se de que não adicione uma barra final **/** no final do URL ou a conexão não funcionará.

1. Verifique se a caixa de seleção **Ativado** está selecionada e clique em **Salvar** para salvar suas modificações.

### Verificação da opção AEMResourceTypeFilter {#verifying-the-aemresourcetypefilter-option}

A opção **AEMResourceTypeFilter** é usada para filtrar tipos de recursos do AEM que podem ser usados no Adobe Campaign. Isso permite que o Adobe Campaign recupere conteúdos do AEM projetados especificamente para serem usados apenas no Adobe Campaign.

Essa opção vem pré-configurada; no entanto, se você alterar essa opção, ela poderá resultar em uma integração inoperante.

Para verificar se a opção **AEMResourceTypeFilter** está configurada:

1. Vá até **Administração** > Configurações **** do aplicativo > **Opções**.
1. Na lista, você pode garantir que a opção **AEMResourceTypeFilter** esteja listada e que os caminhos estejam corretos.

### Criar um template do delivery de email específico do AEM {#creating-an-aem-specific-email-delivery-template}

Por padrão, o recurso AEM não está ativado nos modelos de e-mail do Adobe Campaign. Você pode configurar um novo template do delivery de email que será usado para criar emails com conteúdo do AEM.

Para criar um template do delivery de email específico do AEM:

1. Vá para **Recursos** > **Modelos** > **Templates do delivery**.
1. **Ative a seleção** clicando na marca de seleção na barra de ações e selecionando o modelo padrão de e-mail **padrão (e-mail)** existente, em seguida, duplicado-o clicando no ícone **Copiar** e clicando em **Confirmar**.
1. Desative o modo de seleção clicando no **x** e abra o modelo recém-criado **Copiar do padrão de e-mail (e-mail)** , em seguida, selecione **Editar propriedades** na barra de ação do painel de modelo.

   Você pode modificar o **Rótulo** do modelo.

1. Na seção Propriedades **de conteúdo** , altere a fonte **** de conteúdo para **Adobe Experience Manager**. Em seguida, selecione a conta externa criada anteriormente e clique em **Confirmar**.

   Salve as modificações clicando em **Confirmar** e em **Salvar.**

   Os delivery de e-mail criados a partir deste modelo terão o recurso de conteúdo AEM ativado.

   ![chlimage_1-125](assets/chlimage_1-125a.png)

## Configuring Adobe Experience Manager {#configuring-adobe-experience-manager}

Para configurar o AEM, você deve fazer o seguinte:

* Configure a replicação entre instâncias.
* Conecte o AEM ao Adobe Campaign.
* Configure o externalizador.

### Configuração da replicação entre instâncias do AEM {#configuring-replication-between-aem-instances}

O conteúdo criado na instância de criação do AEM é enviado primeiro para a instância de publicação. Essa instância de publicação transfere o conteúdo para o Adobe Campaign. O agente de replicação deve, portanto, ser configurado para replicar da instância de criação do AEM para a instância de publicação do AEM.

>[!NOTE]
>
>Se você não quiser usar o URL de replicação, mas usar o URL voltado para o público, poderá definir o URL **** público na seguinte configuração no OSGi (**Ferramentas** > Console **da** Web > Configuração **OSGi > Integração de Campanha AEM - Configuração**):
**URL público:** com.day.cq.mcm.campanha.impl.IntegrationConfigImpl#aem.mcm.campanha.publicUrl

Essa etapa também é necessária para replicar determinadas configurações de instância de criação na instância de publicação.

Para configurar a replicação entre instâncias do AEM:

1. Na instância de criação, selecione o logotipo **do** AEM > **Ferramentas** > **Implantação** > **Replicação** > **Agentes do autor****** e clique em Agente padrão.

   ![chlimage_1-126](assets/chlimage_1-126a.png)

   >[!NOTE]
   Evite usar localhost (ou seja, uma cópia local do AEM) ao configurar sua integração com o Adobe Campaign, a menos que as instâncias de publicação e autor estejam ambas no mesmo computador.

1. Clique em **Editar** e selecione a guia **Transporte** .
1. Configure o URI substituindo **localhost** pelo endereço IP ou pelo endereço da instância de publicação do AEM.

   ![chlimage_1-127](assets/chlimage_1-127a.png)

### Conexão do AEM ao Adobe Campaign {#connecting-aem-to-adobe-campaign}

Antes de poder usar o AEM e o Adobe Campaign juntos, você deve estabelecer o link entre as duas soluções para que elas possam se comunicar.

1. Conecte-se à sua instância de criação do AEM.
1. Selecione **Ferramentas** > **Operações** > **Nuvem** > Serviços **** em nuvem e, em seguida, **Configurar agora** na seção Adobe Campaign.

   ![chlimage_1-128](assets/chlimage_1-128a.png)

1. Crie uma nova configuração inserindo um **Título** e clique em **Criar**, ou escolha a configuração existente que você deseja vincular à instância do Adobe Campaign.
1. Edite a configuração para que ela corresponda aos parâmetros da sua instância de Adobe Campaign.

   * **Nome de usuário**: **aemserver**, o operador do pacote de integração do AEM Adobe Campaign usado para estabelecer o link entre as duas soluções.
   * **Senha**: senha do operador Adobe Campaign aemserver. Talvez seja necessário especificar novamente a senha desse operador diretamente no Adobe Campaign.
   * **Ponto** final da API: URL da instância Adobe Campaign.

1. Selecione **Conectar-se ao Adobe Campaign** e clique em **OK**.

   ![chlimage_1-127](assets/chlimage_1-129a.png)

   >[!NOTE]
   Depois de [criar seu email e publicá](/help/sites-authoring/campaign.md)-lo, você precisa publicar novamente a configuração na instância de publicação.

   ![chlimage_1-130](assets/chlimage_1-130a.png)

>[!NOTE]
Se a conexão falhar, verifique o seguinte:
* Você pode encontrar um problema de certificado ao usar uma conexão segura com uma instância do Adobe Campaign (https). Será necessário adicionar o certificado de instância Adobe Campaign ao arquivo **cacerts **do seu JDK.
* Além disso, consulte [Solução de problemas da integração](/help/sites-administering/troubleshooting-campaignintegration.md)do AEM/Adobe Campaign.



### Configuração do externalizador {#configuring-the-externalizer}

É necessário [configurar o externalizador](/help/sites-developing/externalizer.md) no AEM na instância do autor. O Externalizador é um serviço OSGi que permite transformar um caminho de recurso em um URL externo e absoluto. Este serviço fornece um local central para configurar esses URLs externos e criá-los.

Consulte [Configurar o externalizador](/help/sites-developing/externalizer.md) para obter instruções gerais. Para a integração com o Adobe Campaign, certifique-se de configurar o servidor de publicação `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` `localhost:4503` não ponto a ponto, mas para um servidor que possa ser acessado pelo console do Adobe Campaign.

Se ele apontar para `localhost:4503` ou para outro servidor que o Adobe Campaign não possa acessar, suas imagens não aparecerão no console Adobe Campaign.

![chlimage_1-131](assets/chlimage_1-131a.png)

