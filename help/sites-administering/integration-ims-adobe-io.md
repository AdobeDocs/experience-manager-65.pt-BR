---
title: Integração com o Adobe Target usando o Adobe I/O
seo-title: Integration with Adobe Target using Adobe I/O
description: Saiba mais sobre como integrar AEM com o Adobe Target usando o Adobe I/O
seo-description: Learn about integrating AEM with Adobe Target using Adobe I/O
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
exl-id: ba7abc53-7db8-41b1-a0fa-4e4dbbeca402
source-git-commit: baacb6623757c4a7a67ae2be4232a36c4a509b69
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 1%

---

# Integração com o Adobe Target usando o Adobe I/O{#integration-with-adobe-target-using-adobe-i-o}

A integração do AEM com o Adobe Target por meio da API do Target Standard requer a configuração do Adobe IMS (Identity Management System) e do Adobe I/O.

>[!NOTE]
>
>O suporte para a API do Adobe Target Standard é novo no AEM 6.5. A API do Target Standard usa a autenticação IMS.
>
>O uso da API do Adobe Target Classic no AEM ainda é compatível com versões anteriores. A [API do Target Classic usa a autenticação de credenciais de usuário](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).
>
>A seleção da API é orientada pelo método de autenticação usado para a integração do AEM/Target.
>Consulte também a seção [ID do locatário e Código do cliente](#tenant-client) .

## Pré-requisitos {#prerequisites}

Antes de iniciar este procedimento:

* [O ](https://helpx.adobe.com/br/contact/enterprise-support.ec.html) Suporte do Adobe deve provisionar sua conta para:

   * Console Adobe
   * Adobe I/O
   * Adobe Target e
   * Adobe IMS (Sistema Identity Management)

* O Administrador de sistema da sua organização deve usar o Admin Console para adicionar os desenvolvedores necessários em sua organização aos perfis de produto relevantes.

   * Isso fornece aos desenvolvedores específicos permissões para ativar integrações no Adobe I/O.
   * Para obter mais detalhes, consulte [Gerenciar desenvolvedores](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configuração de um IMS - Geração de uma chave pública {#configuring-an-ims-configuration-generating-a-public-key}

O primeiro estágio da configuração é criar uma Configuração IMS no AEM e gerar a Chave pública.

1. Em AEM, abra o menu **Ferramentas**.
1. Na seção **Security** selecione **Adobe IMS Configurations**.
1. Selecione **Create** para abrir a **Configuração de conta técnica do Adobe IMS**.
1. Usando o menu suspenso em **Cloud Configuration**, selecione **Adobe Target**.
1. Ative **Create new certificate** e insira um novo alias.
1. Confirme com **Criar certificado**.

   ![](assets/integrate-target-io-01.png)

1. Selecione **Download** (ou **Baixar chave pública**) para baixar o arquivo na unidade local, de modo que esteja pronto para uso ao configurar o Adobe I/O para integração do Adobe Target com AEM](#configuring-adobe-i-o-for-adobe-target-integration-with-aem).[

   >[!CAUTION]
   >
   >Mantenha essa configuração aberta, ela será necessária novamente ao [Concluir a configuração IMS no AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-02.png)

## Configuração do Adobe I/O para integração do Adobe Target com o AEM {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

Você precisa criar o Adobe I/O Project (integração) com o Adobe Target que AEM usará e, em seguida, atribuir os privilégios necessários.

### Criação do projeto {#creating-the-project}

Abra o console Adobe I/O para criar um Projeto de E/S com o Adobe Target que AEM usará:

>[!NOTE]
>
>Consulte também os [tutoriais do Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html).

1. Abra o console Adobe I/O para Projetos:

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. Quaisquer projetos que você tiver serão mostrados. Selecione **Criar Novo Projeto** - o local e o uso dependerão de:

   * Se você ainda não tiver um projeto, **Criar novo projeto** estará no centro, abaixo.
      ![Criar novo projeto - Primeiro projeto](assets/integration-target-io-02.png)
   * Caso já tenha projetos existentes, eles serão listados e **Criar novo projeto** estará no topo direito.
      ![Criar novo projeto - Vários projetos](assets/integration-target-io-03.png)


1. Selecione **Adicionar ao Projeto** seguido por **API**:

   ![](assets/integration-target-io-10.png)

1. Selecione **Adobe Target**, em seguida **Seguinte**:

   >[!NOTE]
   >
   >Se você estiver inscrito no Adobe Target, mas não o vir listado, deverá verificar os [Pré-requisitos](#prerequisites).

   ![](assets/integration-target-io-12.png)

1. **Carregue sua chave** pública e, ao concluir, continue com  **Próximo**:

   ![](assets/integration-target-io-13.png)

1. Revise as credenciais e continue com **Next**:

   ![](assets/integration-target-io-15.png)

1. Selecione os perfis de produto necessários e continue com **Salvar API configurada**:

   >[!NOTE]
   >
   >Os perfis de produto exibidos com o dependem se você:
   >
   >* Adobe Target Standard - somente **Espaço de trabalho padrão** está disponível
   >* Adobe Target Premium - todos os espaços de trabalho disponíveis são listados, conforme mostrado abaixo


   ![](assets/integration-target-io-16.png)

1. A criação será confirmada.

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### Atribuir privilégios à integração {#assigning-privileges-to-the-integration}

Agora, você deve atribuir os privilégios necessários à integração:

1. Abra o Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Navegue até **Products** (barra de ferramentas superior), em seguida, selecione **Adobe Target - &lt;*your-tenant-id*** (no painel esquerdo).
1. Selecione **Perfis de Produto** e, em seguida, o espaço de trabalho necessário na lista apresentada. Por exemplo, Espaço de trabalho padrão.
1. Selecione **Integrações** e depois a configuração de integração necessária.
1. Selecione **Editor** como a **Função do Produto**; em vez de **Observer**.

## Detalhes armazenados para o Projeto de integração do Adobe I/O {#details-stored-for-the-adobe-io-integration-project}

No console Projetos do Adobe I/O, é possível ver uma lista de todos os seus projetos de integração:

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

Selecione **View** (à direita de uma entrada de projeto específica) para mostrar mais detalhes sobre a configuração. Dentre elas:

* Visão geral do projeto
* Insights
* Credenciais
   * Conta de serviço (JWT)
      * Detalhes da credencial
      * Gerar JWT
* APIS
   * Por exemplo, Adobe Target

Alguns deles, você precisará concluir a integração do Adobe I/O para o Target em AEM.

## Concluir a configuração IMS no AEM {#completing-the-ims-configuration-in-aem}

Ao retornar para AEM, é possível concluir a configuração do IMS adicionando valores necessários da integração do Adobe I/O para o Target:

1. Retorne para [Configuração IMS aberta em AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Selecione **Próximo**.

1. Aqui você pode usar os detalhes [do Adobe I/O](#details-stored-for-the-adobe-io-integration-project):

   * **Título**: Seu texto.
   * **Servidor** de autorização: Copie/cole na  `"aud"` linha da seção  **** Carga abaixo, por exemplo,  `"https://ims-na1.adobelogin.com"` no exemplo abaixo
   * **Chave** da API: Copie isso na seção  [](#details-stored-for-the-adobe-io-integration-project) Visão geral da integração do Adobe I/O para o Target
   * **Segredo** do cliente: Gere isso na seção  [](#details-stored-for-the-adobe-io-integration-project) Visão geral da integração do Adobe I/O para o Target e copie
   * **Carga**: Copie isso da seção  [Gerar ](#details-stored-for-the-adobe-io-integration-project) JWTda integração do Adobe I/O para o Target

   ![](assets/integrate-target-io-10.png)

1. Confirme com **Create**.

1. Sua configuração do Adobe Target será exibida no console AEM.

   ![](assets/integrate-target-io-11.png)

## Confirmação da configuração IMS {#confirming-the-ims-configuration}

Para confirmar que a configuração está funcionando como esperado:

1. Abrir:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Por exemplo:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Selecione sua configuração.
1. Selecione **Verificar integridade** na barra de ferramentas, seguida de **Verificar**.

   ![](assets/integrate-target-io-12.png)

1. Se bem-sucedido, você verá a mensagem:

   ![](assets/integrate-target-io-13.png)

## Configuração do Cloud Service Adobe Target {#configuring-the-adobe-target-cloud-service}

A configuração agora pode ser mencionada para um Cloud Service para usar a API do Target Standard:

1. Abra o menu **Ferramentas**. Em seguida, na seção **Cloud Services**, selecione **Cloud Services herdados**.
1. Role para baixo até **Adobe Target** e selecione **Configurar agora**.

   A caixa de diálogo **Criar configuração** será aberta.

1. Insira um **Title** e, se desejar, um **Name** (se deixado em branco, isso será gerado a partir do título).

   Você também pode selecionar o modelo necessário (se mais de um estiver disponível).

1. Confirme com **Create**.

   A caixa de diálogo **Editar componente** será aberta.

1. Insira os detalhes na guia **Configurações do Adobe Target**:

   * **Autenticação**: IMS
   * **ID** do locatário: a ID de locatário do Adobe IMS. Consulte também a seção [ID do locatário e Código do cliente](#tenant-client) .

      >[!NOTE]
      >
      >Para o IMS, esse valor precisa ser obtido do próprio Target. Você pode fazer logon no Target e extrair a ID do locatário do URL.
      >
      >Por exemplo, se o URL for:
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >Em seguida, você usaria `yourtenantid`.
   * **Código** do cliente: Consulte a ID do  [locatário e a ](#tenant-client) Codesecção do cliente.
   * **Configuração** IMS: selecione o nome da Configuração IMS
   * **Tipo** de API: REST
   * **Configuração** do A4T Analytics Cloud: Selecione a configuração de nuvem do Analytics usada para métricas e metas de atividade do Target. Isso é necessário se estiver usando o Adobe Analytics como fonte de relatórios ao direcionar conteúdo. Se você não vir a configuração da nuvem, consulte a observação em [Configuração do A4T Analytics Cloud](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).
   * **Usar direcionamento** preciso: Por padrão, essa caixa de seleção está marcada. Se selecionada, a configuração do serviço de nuvem aguardará o contexto carregar antes de carregar o conteúdo. Veja a observação a seguir.
   * **Sincronizar segmentos do Adobe Target**: Selecione essa opção para baixar segmentos definidos no Target para usá-los em AEM. Você deve selecionar essa opção quando a propriedade Tipo de API for REST, pois os segmentos em linha não são compatíveis e você sempre precisa usar segmentos do Target. (Observe que o termo AEM de &quot;segmento&quot; equivale ao &quot;público-alvo&quot; do Target.)
   * **Biblioteca** do cliente: Selecione se deseja a biblioteca do cliente AT.js ou mbox.js (obsoleto).
   * **Use o Sistema de gerenciamento de tags para fornecer a biblioteca** do cliente: Use o DTM (obsoleto), o Adobe Launch ou qualquer outro sistema de gerenciamento de tags.
   * **AT.js** personalizada: Deixe em branco se tiver marcado a caixa Tag Management ou para usar a AT.js padrão. Como alternativa, carregue sua AT.js personalizada. Somente será exibido se tiver selecionado AT.js.

   >[!NOTE]
   >
   >[A configuração de um Cloud Service para usar a ](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) API do Target Classic foi substituída (usa a guia Configurações do Adobe Recommendations ).
1. Clique em **Conectar ao Target** para inicializar a conexão com o Adobe Target.

   Se a conexão for bem-sucedida, a mensagem **Connection success** será exibida.

1. Selecione **OK** na mensagem, seguido por **OK** na caixa de diálogo para confirmar a configuração.
1. Agora você pode prosseguir para [Adicionar uma estrutura do Target](/help/sites-administering/target-configuring.md#adding-a-target-framework) para configurar parâmetros do ContextHub ou do ClientContext que serão enviados para o Target. Observe que isso pode não ser necessário para exportar AEM Fragmentos de experiência para o Target.

### ID do locatário e código do cliente {#tenant-client}

Com [Adobe Experience Manager 6.5.8.0](/help/release-notes/sp-release-notes.md), o campo Código do cliente foi adicionado à janela de configuração do Target.

Ao configurar os campos ID do locatário e Código do cliente , esteja ciente do seguinte:

1. Para a maioria dos clientes, a ID do locatário e o código do cliente são os mesmos. Isso significa que ambos os campos contêm as mesmas informações e são idênticos. Certifique-se de inserir a ID do locatário em ambos os campos.
2. Para fins herdados, você também pode inserir valores diferentes nos campos ID do locatário e Código do cliente .

Em ambos os casos, esteja ciente de que:

* Por padrão, o Código do cliente (se adicionado primeiro) também será copiado automaticamente para o campo ID do locatário .
* Você tem a opção de alterar o conjunto padrão de ID de locatário.
* Assim, as chamadas de back-end para o Target serão baseadas na ID do locatário e as chamadas do lado do cliente para o Target serão baseadas no Código do cliente.

Conforme dito anteriormente, o primeiro caso é o mais comum para o AEM 6.5. De qualquer forma, verifique se os campos **ambos** contêm as informações corretas, dependendo de seus requisitos.

>[!NOTE]
>
> Se quiser alterar uma Configuração do Target existente:
>
> 1. Insira novamente a ID do locatário.
> 2. Conecte-se novamente ao Target.
> 3. Salve a configuração.

