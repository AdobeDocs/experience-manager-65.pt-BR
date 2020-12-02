---
title: Integração com o Silverpop Engage
seo-title: Integração com o Silverpop Engage
description: Saiba como integrar AEM com o Silverpop Engage
seo-description: Saiba como integrar AEM com o Silverpop Engage
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
translation-type: tm+mt
source-git-commit: 4e5e6ef022dc9f083859e13ab9c86b622fc3d46e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 2%

---


# Integração com o Silverpop Engage{#integrating-with-silverpop-engage}

>[!NOTE]
>
>A integração do Silverpop está **e não** disponível imediatamente. Você deve baixar o [pacote de integração do Silverpop](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content) do Compartilhamento de pacotes e instalá-lo em sua instância. Depois de instalar o pacote, você pode configurá-lo conforme descrito neste documento.

Integrar AEM com o Silverpop Engage permite gerenciar e enviar emails criados no AEM via Silverpop. Também permite usar os recursos de gerenciamento de lead do Silverpop por meio de formulários AEM em páginas AEM.

A integração oferece os seguintes recursos:

* A capacidade de criar e-mails em AEM e publicá-los no Silverpop para distribuição.
* A capacidade de definir uma ação de um formulário AEM para criar um assinante Silverpop.

Depois que o Silverpop Engage for configurado, você poderá publicar boletins informativos ou emails no Silverpop Engage.

## Criando uma configuração do Silverpop {#creating-a-silverpop-configuration}

As configurações Silverpop podem ser adicionadas por meio de **Cloudservices**, **Ferramentas** ou **pontos finais de API**. Todos os métodos estão descritos nesta seção.

### Configuração do Silverpop via Cloudservices {#configuring-silverpop-via-cloudservices}

Para criar uma configuração Silverpop no Cloud Services:

1. No AEM, toque ou clique em **Ferramentas** > **Implantação** > **Cloud Services**. (Ou acesse diretamente em `https://<hostname>:<port>/etc/cloudservices.html`.)
1. Em serviços de terceiros, clique em **Silverop Engage** e **Configure**. A janela de configuração do Silverpop é aberta.

   >[!NOTE]
   >
   >O Silverpop Engage não está disponível como uma opção em serviços de terceiros, a menos que você baixe o pacote do Compartilhamento de pacotes.

1. Insira um título e, opcionalmente, um nome e clique em **Criar**. A janela de configuração** Silverpop Settings** é aberta.
1. Digite o nome de usuário, a senha e selecione um terminal de API na lista suspensa.
1. Clique em **Conectar-se ao Silverpop.** Quando você se conectou com êxito, verá uma caixa de diálogo de sucesso. Clique em **OK** para sair da janela. Você pode acessar o Silverpop clicando em **Ir para Silverpop Engage**.
1. O Silverpop foi configurado. Você pode editar a configuração clicando em **Editar**.
1. Além disso, a estrutura Silverpop Engage pode ser configurada para ações personalizadas fornecendo título e nome (opcional). Clique em Criar para criar a estrutura para a conexão Silverpop já configurada.

   Colunas de extensão de dados importadas podem ser usadas posteriormente pelo componente AEM - **Texto e Personalização**.

### Configuração do Silverpop via Ferramentas {#configuring-silverpop-via-tools}

Para criar uma configuração Silverpop em Ferramentas:

1. No AEM, toque ou clique em **Ferramentas** > **Implantação** > **Cloud Services**. Ou navegue diretamente para lá indo para `https://<hostname>:<port>/misadmin#/etc`.
1. Selecione **Ferramentas**, em seguida **Configurações de Cloud Services,** em seguida **Silverpop Engage**.
1. Clique em **Novo** para abrir a janela **Criar página**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. Digite o **Título** e opcionalmente o **Nome** e clique em **Criar**.
1. Digite as informações de configuração conforme descrito na etapa 4 do procedimento anterior. Siga esse procedimento para concluir a configuração do Silverpop.

### Adicionar várias configurações {#adding-multiple-configurations}

Para adicionar várias configurações:

1. Na página de boas-vindas, clique em **Cloud Services** e em **Silverpop Engage**. Clique no botão **Mostrar configurações** que será exibido se uma ou mais configurações Silverpop estiverem disponíveis. Todas as configurações disponíveis são listadas.
1. Clique no sinal de **+** ao lado de Configurações disponíveis. Isso abre a janela **Criar configurações**. Siga o procedimento de configuração anterior para criar uma nova configuração.

### Configurando pontos finais de API para conexão com o Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

Atualmente, AEM tem seis pontos finais não protegidos (participação de 1 a 6). O Silverpop agora fornece dois novos pontos finais, bem como pontos finais de conexão alterados para os existentes.

Para configurar os pontos finais da API:

1. Ir para `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` em `https://<hostname>:<port>/crxde.`
1. Clique com o botão direito do mouse e selecione **Criar**, em seguida **Criar nó**.
1. Digite **Name** como `sp-e0` e escolha **Type** como `cq:Widget`.
1. Adicione duas propriedades ao nó recém-adicionado:

   1. **Nome**:  `text`,  **Tipo**:  `String`,  **Valor**:  `Engage 0`
   1. **Nome**:  `value`,  **Tipo**:  `String`,  **Valor**:  `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   Clique no botão &quot;Salvar tudo&quot;.

1. Crie mais um nó com **Name** como `sp-e7` e **Type** como `cq:Widget`.

   Adicione duas propriedades ao nó recém-adicionado:

   1. **Nome**:  `text`,  **Tipo**:  `String`,  **Valor**:  `Pilot`
   1. **Nome**:  `value`,  **Tipo**:  `String`,  **Valor**:  `https://apipilot.silverpop.com/XMLAPI`

1. Para alterar os pontos finais da API (participação de 1 a 6), clique em cada um deles e substitua os valores da seguinte maneira:

   | **Nome do nó** | **Valor do Ponto Final Existente** | **Novo Valor de Ponto Final** |
   |---|---|---|
   | sp-e1 | https://api.engage1.silverpop.com/XMLAPI | https://api1.silverpop.com |
   | sp-e2 | https://api.engage2.silverpop.com/XMLAPI | https://api2.silverpop.com |
   | sp-e3 | https://api.engage3.silverpop.com/XMLAPI | https://api3.silverpop.com |
   | sp-e4 | https://api.engage4.silverpop.com/XMLAPI | https://api4.silverpop.com |
   | sp-e5 | https://api.engage5.silverpop.com/XMLAPI | https://api5.silverpop.com |
   | sp-e6 | https://api.pilot.silverpop.com/XMLAPI | https://api6.silverpop.com |

1. Clique em **Salvar tudo**. AEM agora está pronto para se conectar ao Silverpop em pontos finais protegidos.

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)

