---
title: Integração com o Adobe Campaign Classic
seo-title: Integração com o Adobe Campaign Classic
description: Saiba como integrar o AEM ao Adobe Campaign Classic
seo-description: Saiba como integrar o AEM ao Adobe Campaign Classic
uuid: 3c998b0e-a885-4aa9-b2a4-81b86f9327d3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: df94dd1b-1b65-478b-a28d-81807a8084b1
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# Integração com o Adobe Campaign Classic{#integrating-with-adobe-campaign-classic}

>[!NOTE]
>
>Esta documentação descreve como integrar o AEM ao Adobe Campaign Classic, a solução local. Se você estiver usando o Adobe Campaign Standard, consulte [Integração com o Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) para obter essas instruções.

O Adobe Campaign permite gerenciar o conteúdo e os formulários de entrega por email diretamente no Adobe Experience Manager.

Para usar as duas soluções juntas ao mesmo tempo, primeiro configure-as para se conectarem umas às outras. Isso envolve etapas de configuração no Adobe Campaign e no Adobe Experience Manager. Essas etapas são descritas detalhadamente neste documento.

Trabalhar com o Adobe Campaign no AEM inclui a capacidade de enviar emails por meio do Adobe Campaign e está descrita em [Trabalhar com o Adobe Campaign](/help/sites-authoring/campaign.md). Também inclui o uso de formulários em páginas do AEM para manipular dados.

Além disso, os seguintes tópicos podem ser de interesse ao integrar o AEM ao [Adobe Campaign](https://helpx.adobe.com/support/campaign/classic.html):

* [Práticas recomendadas para modelos de e-mail](/help/sites-administering/best-practices-for-email-templates.md)
* [Solução de problemas da integração do Adobe Campaign](/help/sites-administering/troubleshooting-campaignintegration.md)

Se você estiver estendendo a integração com o Adobe Campaign, talvez deseje ver as seguintes páginas:

* [Criação de extensões personalizadas](/help/sites-developing/extending-campaign-extensions.md)
* [Criação de mapeamentos de formulário personalizados](/help/sites-developing/extending-campaign-form-mapping.md)

## Fluxo de trabalho de integração do AEM e do Adobe Campaign {#aem-and-adobe-campaign-integration-workflow}

Esta seção descreve um fluxo de trabalho típico entre o AEM e o Adobe Campaign ao criar campanhas e fornecer conteúdo.

O fluxo de trabalho típico envolve o seguinte e é descrito em detalhes:

1. Comece a criar sua campanha (tanto no Adobe Campaign quanto no AEM).
1. Antes de vincular o conteúdo e a entrega, personalize seu conteúdo no AEM e crie uma entrega no Adobe Campaign.
1. Vincule conteúdo e entrega no Adobe Campaign.

### Comece a criar sua campanha {#start-building-your-campaign}

Você começa a criar uma campanha a qualquer momento. Antes de vincular o conteúdo, o AEM e o AC são independentes. Isso significa que os profissionais de marketing podem começar a criar suas campanhas e direcionamento no Adobe Campaign, enquanto os criadores de conteúdo estão trabalhando no design no AEM.

### Antes de vincular o conteúdo e a entrega {#before-linking-content-and-delivery}

Antes de vincular o conteúdo e criar um mecanismo de entrega, é necessário fazer o seguinte:

**No AEM**

* Personalizar usando os campos de personalização no componente **Texto e personalização**

**No Adobe Campaign**

* Criar uma entrega do tipo **aemContent**

### Vincular conteúdo e configurar entrega {#linking-content-and-setting-delivery}

Depois de preparar o conteúdo para vinculação e entrega, você determina exatamente como e onde vincular o conteúdo.

Todas essas etapas foram concluídas no Adobe Campaign.

1. Especifique qual instância do AEM usar.
1. Sincronize o conteúdo clicando no botão Sincronizar.
1. Abra o seletor de conteúdo para selecionar seu conteúdo.

### Se você for novo no AEM {#if-you-are-new-to-aem}

Se você for novo no AEM, talvez ache os seguintes links úteis para entender o AEM:

* [Iniciar o AEM](/help/sites-deploying/deploy.md)
* [Noções básicas sobre os agentes de replicação](/help/sites-deploying/replication.md)
* [Como localizar e trabalhar com arquivos de registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)
* [Introdução à plataforma AEM](/help/sites-deploying/platform.md)

## Configuração do Adobe Campaign {#configuring-adobe-campaign}

A configuração do Adobe Campaign envolve o seguinte:

1. Instalação do pacote de integração do AEM no Adobe Campaign.
1. Configuração de uma conta externa.
1. Verificando se AEMResourceTypeFilter está configurado corretamente.

Além disso, há configurações avançadas que você pode fazer, incluindo:

* Gerenciamento de blocos de conteúdo
* Gerenciamento de campos de personalização

Consulte Configurações [avançadas](#advanced-configurations).

>[!NOTE]
>
>Para executar essas operações, é necessário ter a função de **administração** no Adobe Campaign.

### Pré-requisitos {#prerequisites}

Verifique se você tem os seguintes elementos antecipadamente:

* [Uma instância de criação do AEM](/help/sites-deploying/deploy.md#getting-started)
* [Uma instância de publicação do AEM](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Uma instância](https://helpx.adobe.com/support/campaign/classic.html) do Adobe Campaign Classic - incluindo um cliente e um servidor
* Internet Explorer 11

>[!NOTE]
>
>Se você estiver executando uma versão anterior ao Adobe Campaign Classic build 8640, consulte a documentação [de](https://docs.campaign.adobe.com/doc/AC6.1/en/PRO_Updating_Adobe_Campaign_Upgrading.html) atualização para obter mais informações. Observe que tanto o cliente quanto o banco de dados precisam ser atualizados para a mesma compilação.

>[!CAUTION]
>
>As operações detalhadas nas seções [Configuração do Adobe Campaign](#configuring-adobe-campaign) e [Configuração do Adobe Experience Manager](#configuring-adobe-experience-manager) são necessárias para que as funcionalidades de integração entre o AEM e o Adobe Campaign funcionem corretamente.

### Instalação do pacote de integração do AEM {#installing-the-aem-integration-package}

Você deve instalar o pacote de integração **do** AEM no Adobe Campaign. Para fazer isso:

1. Vá para a instância do Adobe Campaign que você deseja vincular ao AEM.
1. *Selecione* Ferramentas *>* Avançado *>* Importar pacote... .

   ![chlimage_1-132](assets/chlimage_1-132a.png)

1. Clique em **Instalar um pacote** padrão e selecione o pacote de integração **do** AEM.

   ![chlimage_1-133](assets/chlimage_1-133a.png)

1. Clique em **Avançar** e em **Iniciar**.

   Este pacote contém o operador **aemserver** que será usado para conectar o servidor AEM ao Adobe Campaign.

   >[!CAUTION]
   >
   >Por padrão, nenhuma zona de segurança está configurada para esse operador. Para se conectar ao Adobe Campaign via AEM, é necessário selecionar um.
   >
   >No arquivo **serverConf.xml** , o atributo **allowUserPassword** da zona de segurança selecionada deve ser definido como **true** para autorizar o AEM a conectar o Adobe Campaign via logon/senha.
   >
   >Recomendamos criar uma zona de segurança dedicada ao AEM para evitar problemas de segurança. Para obter mais informações, consulte o guia [](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Configuring_Campaign_server.html)de instalação.

   ![chlimage_1-134](assets/chlimage_1-134a.png)

### Configurar uma conta externa AEM {#configuring-an-aem-external-account}

Você deve configurar uma conta externa que permita conectar o Adobe Campaign à sua instância do AEM.

>[!NOTE]
>
>* Ao instalar o pacote de integração **do** AEM, uma conta externa do AEM é criada. Você pode configurar a conexão com sua instância do AEM a partir dela ou criar uma nova.
>* No AEM, certifique-se de definir a senha para o usuário remoto da campanha. É necessário definir essa senha para conectar o Adobe Campaign ao AEM. Faça logon como administrador e no console de administração do usuário, procure o usuário remoto da campanha e clique em **Definir senha**.
>



Para configurar uma conta AEM externa:

1. Vá para o nó **Administração** > **Plataforma** > Contas **** externas.
1. Crie uma nova conta externa e selecione o tipo de **AEM** .
1. Digite os parâmetros de acesso para a instância de criação do AEM: o endereço do servidor, bem como a ID e a senha usadas para se conectar a esta instância. A senha da conta de usuário api da campanha é a mesma do usuário remoto da campanha para o qual você definiu uma senha no AEM.

   >[!NOTE]
   >
   >Verifique se o endereço do servidor **não** termina em uma barra à direita. Por exemplo, digite `https://yourserver:4502` em vez de `https://yourserver:4502/`

   ![chlimage_1-135](assets/chlimage_1-135a.png) ![chlimage_1-136](assets/chlimage_1-136a.png)

1. Verifique se a caixa de seleção **Ativado** está selecionada.

### Verificação da opção AEMResourceTypeFilter {#verifying-the-aemresourcetypefilter-option}

A opção **AEMResourceTypeFilter** é usada para filtrar tipos de recursos AEM que podem ser usados no Adobe Campaign. Isso permite que o Adobe Campaign recupere conteúdos do AEM projetados especificamente para serem usados somente no Adobe Campaign.

Essa opção deve vir pré-configurada; no entanto, se você alterar essa opção, ela poderá resultar em uma integração inoperante.

Para verificar se a opção **AEMResourceTypeFilter** está configurada:

1. Vá para **Plataforma** >**Opções**.
1. Na opção **AEMResourceTypeFilter** , verifique se os caminhos estão corretos. Este campo deve conter o valor:

   **mcm/campaign/components/newsletter,mcm/campaign/components/campaign_newsletterpage,mcm/neolane/components/newsletter**

   Ou, em alguns casos, o valor é o seguinte:

   **mcm/campaign/components/newsletter**

   ![chlimage_1-137](assets/chlimage_1-137a.png)

## Configuring Adobe Experience Manager {#configuring-adobe-experience-manager}

Para configurar o AEM, você deve fazer o seguinte:

* Configure a replicação entre instâncias.
* Conecte o AEM ao Adobe Campaign por meio dos serviços em nuvem.
* Configure o externalizador.

### Configuração da replicação entre instâncias do AEM {#configuring-replication-between-aem-instances}

O conteúdo criado na instância de criação do AEM é enviado primeiro para a instância de publicação. É necessário publicar para que as imagens no boletim informativo estejam disponíveis na instância de publicação e para os destinatários do boletim. O agente de replicação deve, portanto, ser configurado para replicar da instância de criação do AEM para a instância de publicação do AEM.

>[!NOTE]
>
>Se você não quiser usar o URL de replicação, mas em vez disso usar o URL voltado para o público, poderá definir o URL **** público na seguinte configuração no OSGi (logo **do** AEM > ícone **Ferramentas** > **Operações** > Console **da** **** **** Web > Configuração do OSGi > Integração de campanha do AEM - Configuração):
**** URL público: com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

Essa etapa também é necessária para replicar determinadas configurações de instância de criação na instância de publicação.

Para configurar a replicação entre instâncias do AEM:

1. Na instância de criação, selecione o logotipo **do** AEM > ícone **Ferramentas** > **Implantação** > **Replicação** > **Agentes do autor****** e clique em Agente padrão.

   ![chlimage_1-138](assets/chlimage_1-138a.png)

   >[!NOTE]
   Evite usar localhost (ou seja, uma cópia local do AEM) ao configurar sua integração com o Adobe Campaign, a menos que as instâncias de publicação e autor estejam ambas no mesmo computador.

1. Toque ou clique em **Editar** e selecione a guia **Transporte** .
1. Configure o URI substituindo **localhost** pelo endereço IP ou pelo endereço da instância de publicação do AEM.

   ![chlimage_1-139](assets/chlimage_1-139a.png)

### Conexão do AEM ao Adobe Campaign {#connecting-aem-to-adobe-campaign}

Antes de poder usar o AEM e o Adobe Campaign juntos, você deve estabelecer o link entre as duas soluções para que elas possam se comunicar.

1. Conecte-se à sua instância de criação do AEM.
1. Selecione o logotipo **do** AEM > ícone **Ferramentas** > **Implantação** > Serviços **** em nuvem e, em seguida, **Configurar agora** na seção Adobe Campaign.

   ![chlimage_1-140](assets/chlimage_1-140a.png)

1. Crie uma nova configuração inserindo um **Título** e clique em **Criar**, ou escolha a configuração existente que deseja vincular à instância do Adobe Campaign.
1. Edite a configuração para que ela corresponda aos parâmetros da sua instância do Adobe Campaign.

   * **Nome de usuário**: **aemserver**, o operador do pacote de integração do Adobe Campaign AEM usado para estabelecer o link entre as duas soluções.
   * **Senha**: Senha do operador do servidor do Adobe Campaign. Talvez seja necessário especificar novamente a senha desse operador diretamente no Adobe Campaign.
   * **Ponto** final da API: URL da instância do Adobe Campaign.

1. Selecione **Conectar-se ao Adobe Campaign** e clique em **OK**.

   ![chlimage_1-141](assets/chlimage_1-141a.png)

   >[!NOTE]
   Depois de [criar seu email e publicá](/help/sites-authoring/campaign.md)-lo, você precisa publicar novamente a configuração na instância de publicação.

   ![chlimage_1-142](assets/chlimage_1-142a.png)

>[!NOTE]
Se a conexão falhar, verifique o seguinte:
* Você pode encontrar um problema de certificado ao usar uma conexão segura com uma instância do Adobe Campaign (https). Você precisará adicionar o certificado de instância do Adobe Campaign ao arquivo **cacerts** do JDK da instância do AEM.
* Uma zona de segurança deve ser configurada para o operador [aemserver](#connecting-aem-to-adobe-campaign) no Adobe Campaign. Além disso, no arquivo **serverConf.xml** , o atributo **allowUserPassword** da zona de segurança deve ser definido como **true** para autorizar a conexão do AEM com o Adobe Campaign usando o modo de logon/senha.

Além disso, consulte [Solução de problemas da integração](/help/sites-administering/troubleshooting-campaignintegration.md)do AEM/Adobe Campaign.

### Configuração do externalizador {#configuring-the-externalizer}

É necessário [configurar o externalizador](/help/sites-developing/externalizer.md) no AEM na instância do autor. O Externalizador é um serviço OSGi que permite transformar um caminho de recurso em um URL externo e absoluto. Este serviço fornece um local central para configurar esses URLs externos e criá-los.

Consulte [Configurar o externalizador](/help/sites-developing/externalizer.md) para obter instruções gerais. Para a integração do Adobe Campaign, certifique-se de configurar o servidor de publicação `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`não aponte para `localhost:4503` mas para um servidor que possa ser acessado pelo console do Adobe Campaign.

Se ele apontar para `localhost:4503` ou para outro servidor que o Adobe Campaign não consegue acessar, suas imagens não aparecerão no console do Adobe Campaign.

![chlimage_1-143](assets/chlimage_1-143a.png)

## Configurações avançadas {#advanced-configurations}

Você também pode executar algumas configurações avançadas, a saber:

* Gerencie campos e blocos de personalização.
* Desative um bloco de personalização.
* Gerenciar dados de extensão de destino.

### Gerenciamento de campos e blocos de personalização {#managing-personalization-fields-and-blocks}

Os campos e blocos disponíveis para adicionar personalização ao seu conteúdo de email no AEM são gerenciados pelo Adobe Campaign.

Uma lista padrão é fornecida, mas pode ser modificada. Também é possível adicionar ou ocultar campos e blocos de personalização.

#### Adicionar um campo de personalização {#adding-a-personalization-field}

Para adicionar um novo campo de personalização àqueles que já estão disponíveis, é necessário estender o esquema Adobe Campaign **nms:sementeMember** da seguinte maneira:

>[!CAUTION]
O campo que você precisa adicionar já deve ter sido adicionado por meio de uma extensão de esquema do destinatário (**nms:receipt**). Para obter mais informações, consulte o guia [Configuração](https://docs.campaign.adobe.com/doc/AC6.1/en/CFG_Editing_schemas_Editing_schemas.html) .

1. Vá para o nó **Administração** > **Configuração** > Esquemas **de** dados na navegação do Adobe Campaign.
1. Selecione **Novo**.

   ![chlimage_1-144](assets/chlimage_1-144a.png)

1. Na janela pop-up, selecione **Estender os dados na tabela usando um esquema** de extensão e clique em **Avançar**.

   ![chlimage_1-145](assets/chlimage_1-145a.png)

1. Informe os diferentes parâmetros do esquema estendido:

   * **Esquema**: selecione o esquema **nms:sementeMember** . Os outros campos na janela são automaticamente concluídos.
   * **Namespace**: personalize o namespace do esquema estendido.

1. Edite o código XML do esquema para especificar o campo que deseja adicionar. Para obter mais informações sobre como estender esquemas no Adobe Campaign, consulte o guia [](https://docs.campaign.adobe.com/doc/AC6.1/en/CFG_Editing_schemas_Extending_a_schema.html)Configuração.
1. Salve o esquema e atualize a estrutura do banco de dados do Adobe Campaign por meio do menu **Ferramentas** > **Avançado** > **Atualizar estrutura** do banco de dados no console.
1. Desconecte e reconecte-se ao console do Adobe Campaign para salvar as alterações. O novo campo agora aparece na lista de campos de personalização disponíveis no AEM.

#### Exemplo {#example}

Para adicionar um campo Número **de** registro, você deve ter os seguintes elementos:

* A extensão de esquema **nms:receipt** chamada **cus:customer** contém:

```xml
<element desc="Recipient table (profiles)" img="nms:recipient.png" label="Recipients" labelSingular="Recipient" name="recipient">

  <attribute dataPolicy="smartCase" desc="Recipient registration number"
  label="Registration Number"
  length="50" name="registrationNumber" type="string"/>

</element>
```

A extensão de esquema **nms:sementeMember** chamada **cus:sementeMember** contém:

```xml
<element desc="Seed to insert in the export files" img="nms:unknownad.png" label="Seed addresses" labelSingular="Seed" name="seedMember">

  <element name="custom_nms_recipient">
    <attribute name="registrationNumber"
    template="cus:recipient:recipient/@registrationNumber"/>
  </element>

</element>
```

O campo Número **de** registro agora faz parte dos campos de personalização disponíveis:

![chlimage_1-146](assets/chlimage_1-146.png)

#### Ocultar um campo de personalização {#hiding-a-personalization-field}

Para ocultar um campo de personalização entre os que já estão disponíveis, você deve estender o esquema **nms:sementeMember** do Adobe Campaign, conforme detalhado na seção [Adicionar um campo](#adding-a-personalization-field) de personalização. Aplique as seguintes etapas:

1. Copie o campo que deseja obter do esquema **nms:sementeMember** no esquema estendido (**cus:sementeMember** , por exemplo).
1. Adicione o atributo XML **advanced=&quot;true&quot;** ao campo. Ela não aparece mais na lista de campos de personalização disponíveis no AEM.

   Por exemplo, para ocultar o campo Nome **do** Meio, o esquema **cud:sementeMember** deve conter o seguinte elemento:

   ```xml
   <element desc="Seed to insert in the export files" img="nms:unknownad.png" label="Seed addresses" labelSingular="Seed" name="seedMember">
   
     <element name="custom_nms_recipient">
       <attribute advanced="true" name="middleName"/>
     </element>
   
   </element>
   ```

### Desativação de um bloco de personalização {#deactivating-a-personalization-block}

Para desativar um bloco de personalização entre os disponíveis:

1. Vá para o nó **Recursos** > Gerenciamento **de** campanha > Blocos **de** personalização na navegação do Adobe Campaign.
1. Selecione o bloco de personalização que deseja desativar no AEM.
1. Desmarque a caixa de seleção **Visível nos menus** de personalização e salve as alterações. O bloco não aparece mais na lista de blocos de personalização disponíveis no Adobe Campaign.

   ![chlimage_1-147](assets/chlimage_1-147a.png)

### Gerenciamento de dados de extensão de destino {#managing-target-extension-data}

Também é possível inserir dados de extensão de destino para personalização. Os dados de extensão do Target (também chamados de &quot;Dados do Target&quot;) vêm do enriquecimento ou adição de dados em uma consulta em um fluxo de trabalho de campanha, por exemplo. Para obter mais informações, consulte as seções [Criação de consultas](https://docs.campaign.adobe.com/doc/AC/en/PTF_Creating_queries_About_queries_in_Campaign.html) e [Enriquecimento de dados](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Enriching_data.html) .

>[!NOTE]
Os dados no destino só estarão disponíveis se o conteúdo do AEM for sincronizado com uma entrega do Adobe Campaign. See [Synchronizing content created in AEM with a delivery from Adobe Campaign](/help/sites-authoring/campaign.md#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic).

![chlimage_1-148](assets/chlimage_1-148a.png)

