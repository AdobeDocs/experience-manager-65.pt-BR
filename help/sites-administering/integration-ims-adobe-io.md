---
title: Integração com a Adobe Target usando E/S Adobe
seo-title: Integração com a Adobe Target usando E/S Adobe
description: Saiba mais sobre como integrar AEM com a Adobe Target usando E/S Adobe
seo-description: Saiba mais sobre como integrar AEM com a Adobe Target usando E/S Adobe
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
translation-type: tm+mt
source-git-commit: 26efba567985dcb89b2610935cab18943b7034b3
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 1%

---


# Integração com a Adobe Target usando E/S Adobe{#integration-with-adobe-target-using-adobe-i-o}

A integração do AEM com o Adobe Target por meio da API do Target Standard requer a configuração do Adobe IMS (Identity Management System) e da E/S do Adobe.

>[!NOTE]
>
>O suporte para a Adobe Target Standard API é novo no AEM 6.5. A API do Target Standard usa autenticação IMS.
>
>O uso da Adobe Target Classic API no AEM ainda é compatível com compatibilidade retroativa. A API [Público alvo Classic usa autenticação](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)de credenciais de usuário.
>
>A seleção da API é orientada pelo método de autenticação usado para integração de AEM/Público alvo.

## Pré-requisitos {#prerequisites}

Antes de iniciar este procedimento:

* [O suporte](https://helpx.adobe.com/br/contact/enterprise-support.ec.html) a Adobe deve fornecer sua conta para:

   * Console Adobe
   * E/S Adobe
   * Adobe Target e
   * Adobe IMS (Sistema Identity Management)

* O Administrador de sistemas da sua organização deve usar o Admin Console para adicionar os desenvolvedores necessários em sua organização aos perfis de produtos relevantes.

   * Isso fornece aos desenvolvedores específicos permissões para permitir integrações dentro da E/S do Adobe.
   * Para obter mais detalhes, consulte [Gerenciar desenvolvedores](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configuração de IMS - Geração de uma chave pública {#configuring-an-ims-configuration-generating-a-public-key}

A primeira etapa da configuração é criar uma Configuração IMS no AEM e gerar a Chave pública.

1. AEM abra o menu **Ferramentas** .
1. Na seção **Segurança** , selecione Configurações **IMS** de Adobe.
1. Selecione **Criar** para abrir a Configuração **de conta técnica do** Adobe IMS.
1. Usando o menu suspenso em Configuração **da** nuvem, selecione **Adobe Target**.
1. Ativar **Criar novo certificado** e inserir um novo alias.
1. Confirme com **Criar certificado**.

   ![](assets/integrate-target-io-01.png)

1. Selecione **Baixar** (ou **Baixar chave** pública) para baixar o arquivo na unidade local, de modo que ele esteja pronto para uso ao [configurar a integração de E/S de Adobe para Adobe Target com AEM](#configuring-adobe-i-o-for-adobe-target-integration-with-aem).

   >[!CAUTION]
   >
   >Mantenha essa configuração aberta, ela será necessária novamente ao [Concluir a configuração do IMS no AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-02.png)

## Configuração de E/S de Adobe para integração do Adobe Target com AEM {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

É necessário criar o Adobe I/O Project (integração) com a Adobe Target que AEM usará e, em seguida, atribuir os privilégios necessários.

### Criação do projeto {#creating-the-project}

Abra o console E/S do Adobe para criar um Projeto de E/S com a Adobe Target que AEM usará:

>[!NOTE]
>
>Consulte também os tutoriais [de E/S do](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html)Adobe.

1. Abra o console E/S do Adobe para Projetos:

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. Todos os projetos que você tiver serão mostrados. Selecione **Criar novo projeto** - o local e o uso dependerão de:

   * Se você ainda não tiver um projeto, a opção **Criar novo projeto** estará no centro, na parte inferior.
      ![Criar novo projeto - Primeiro projeto](assets/integration-target-io-02.png)
   * Se você já tiver projetos existentes, eles serão listados e a opção **Criar novo projeto** estará na parte superior direita.
      ![Criar novo projeto - Vários projetos](assets/integration-target-io-03.png)


1. Selecione **Adicionar ao projeto** seguido de **API**:

   ![](assets/integration-target-io-10.png)

1. Selecione **Adobe Target** e, em seguida, **Próximo**:

   >[!NOTE]
   >
   >Se você estiver inscrito no Adobe Target, mas não o vir listado, verifique os [Pré-requisitos](#prerequisites).

   ![](assets/integration-target-io-12.png)

1. **Carregue sua chave** pública e, ao concluir, continue com **Próximo**:

   ![](assets/integration-target-io-13.png)

1. Revise as credenciais e continue com **Próximo**:

   ![](assets/integration-target-io-15.png)

1. Selecione os perfis de produto necessários e continue com a API **** Salvar configurada:

   >[!NOTE]
   >
   >Os perfis de produto exibidos dependem se você:
   >
   >* Adobe Target Standard - somente Espaço de trabalho **** padrão está disponível
   >* Adobe Target Premium - todos os espaços de trabalho disponíveis são listados, como mostrado abaixo


   ![](assets/integration-target-io-16.png)

1. A criação será confirmada.

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### Atribuindo privilégios à integração {#assigning-privileges-to-the-integration}

Agora, você deve atribuir os privilégios necessários à integração:

1. Abra o Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Navegue até **Produtos** (barra de ferramentas superior) e selecione **Adobe Target - &lt;*your-locatário-id*>** (no painel esquerdo).
1. Selecione Perfis **de** produto e, em seguida, seu espaço de trabalho necessário na lista apresentada. Por exemplo, Espaço de trabalho padrão.
1. Selecione **Integrações** e, em seguida, a configuração de integração necessária.
1. Selecione **Editor** como a Função **** do Produto; em vez de **Observer**.

## Detalhes armazenados para o Projeto de integração de E/S de Adobe {#details-stored-for-the-adobe-io-integration-project}

No console Projetos de E/S de Adobe, você pode ver uma lista de todos os projetos de integração:

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

Selecione **Visualização** (à direita de uma entrada de projeto específica) para mostrar mais detalhes sobre a configuração. Dentre elas:

* Visão geral do projeto
* Insights
* Credenciais
   * Conta de serviço (JWT)
      * Detalhes da credencial
      * Gerar JWT
* APIS
   * Por exemplo, Adobe Target

Alguns deles, você precisará concluir a integração de E/S do Adobe para o Público alvo no AEM.

## Concluindo a configuração do IMS em AEM {#completing-the-ims-configuration-in-aem}

Retornando ao AEM, é possível concluir a configuração do IMS adicionando os valores necessários da integração de E/S do Adobe para o Público alvo:

1. Retorne à Configuração [IMS aberta no AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Selecione **Próximo**.

1. Aqui você pode usar os [detalhes da E/S](#details-stored-for-the-adobe-io-integration-project)do Adobe:

   * **Título**: Seu texto.
   * **Servidor** de autorização: Copie/cole na `"aud"` linha da seção **Carga** abaixo, por exemplo, `"https://ims-na1.adobelogin.com"` no exemplo abaixo
   * **Chave** da API: Copie isso da seção [Visão geral](#details-stored-for-the-adobe-io-integration-project) da integração de E/S do Adobe para o Público alvo
   * **Segredo** do cliente: Gere isso na seção [Visão geral](#details-stored-for-the-adobe-io-integration-project) da integração de E/S do Adobe para o Público alvo e copie
   * **Carga**: Copie-o da seção [Gerar JWT](#details-stored-for-the-adobe-io-integration-project) da integração de E/S do Adobe para o Público alvo

   ![](assets/integrate-target-io-10.png)

1. Confirme com **Criar**.

1. Sua configuração do Adobe Target será exibida no console AEM.

   ![](assets/integrate-target-io-11.png)

## Confirmando a configuração do IMS {#confirming-the-ims-configuration}

Para confirmar se a configuração está funcionando como esperado:

1. Abrir:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Por exemplo:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Selecione sua configuração.
1. Selecione **Verificar integridade** na barra de ferramentas, seguida por **Verificar**.

   ![](assets/integrate-target-io-12.png)

1. Se bem-sucedido, você verá a mensagem:

   ![](assets/integrate-target-io-13.png)

## Configuração do Cloud Service Adobe Target {#configuring-the-adobe-target-cloud-service}

A configuração agora pode ser referenciada para uma Cloud Service para usar a API do Target Standard:

1. Abra o menu **Ferramentas** . Em seguida, na seção **Cloud Services** , selecione **Cloud Services** herdados.
1. Role para baixo até **Adobe Target** e selecione **Configurar agora**.

   The **Create Configuration** dialog will open.

1. Insira um **Título** e, se desejar, um **Nome** (se deixado em branco, isso será gerado a partir do título).

   Você também pode selecionar o modelo necessário (se houver mais de um disponível).

1. Confirme com **Criar**.

   A caixa de diálogo **Editar componente** será aberta.

1. Digite os detalhes na guia Configurações **do** Adobe Target:

   * **Autenticação**: IMS
   * **ID** do inquilino: a ID do locatário do Adobe IMS

      >[!NOTE]
      >
      >Para o IMS este valor precisa ser retirado do próprio Público alvo. Você pode fazer logon no Público alvo e extrair a ID do locatário do URL.
      >
      >Por exemplo, se o URL for:
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >Então você usaria `yourtenantid`.

   * **Configuração** IMS: selecione o nome da Configuração IMS
   * **Tipo** de API: REST
   * **Configuração** Analytics Cloud A4T: Selecione a configuração de nuvem do Analytics usada para as métricas e metas de atividade do público alvo. Isso é necessário se você estiver usando o Adobe Analytics como a fonte do relatórios ao direcionar o conteúdo. Se você não vir a configuração da nuvem, consulte a observação em [Configuração](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration)da A4T Analytics Cloud.
   * **Usar direcionamento** preciso: Por padrão, essa caixa de seleção é selecionada. Se selecionada, a configuração do serviço de nuvem aguardará o contexto ser carregado antes de carregar o conteúdo. Veja a seguir.
   * **Sincronizar segmentos do Adobe Target**: Selecione essa opção para baixar segmentos definidos no Público alvo para usá-los no AEM. Você deve selecionar essa opção quando a propriedade Tipo de API for REST, pois os segmentos em linha não são suportados e você sempre precisa usar os segmentos do Público alvo. (Observe que o termo AEM de &quot;segment&quot; equivale à &quot;audiência&quot; do Público alvo.)
   * **Biblioteca** do cliente: Selecione se deseja a biblioteca do cliente AT.js ou mbox.js (obsoleto).
   * **Use o Sistema de gerenciamento de tags para fornecer a biblioteca** do cliente: Use o DTM (obsoleto), o Adobe Launch ou qualquer outro sistema de gerenciamento de tags.
   * **AT.js** personalizado: Deixe em branco se você tiver marcado a caixa Gerenciamento de tags ou para usar o padrão AT.js. Como alternativa, carregue seu AT.js personalizado. Será exibido somente se você tiver selecionado AT.js.

   >[!NOTE]
   >
   >[A configuração de um Cloud Service para usar a API](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) do Público alvo Classic foi substituída (usa a guia Configurações do Adobe Recommendations).

   Por exemplo:

   ![](assets/integrate-target-io-14.png)

1. Clique em **Conectar-se ao Público alvo** para inicializar a conexão com o Adobe Target.

   Se a conexão for bem-sucedida, será exibida a mensagem **Conexão bem-sucedida** .

1. Selecione **OK** na mensagem, seguido por **OK** na caixa de diálogo para confirmar a configuração.
1. Agora você pode continuar a [Adicionar uma Estrutura](/help/sites-administering/target-configuring.md#adding-a-target-framework) de Públicos alvos para configurar parâmetros do ContextHub ou do ClientContext que serão enviados para o Público alvo. Observe que isso pode não ser necessário para exportar AEM Fragmentos de experiência para o Público alvo.

