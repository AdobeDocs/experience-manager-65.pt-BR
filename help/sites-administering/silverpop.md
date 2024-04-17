---
title: Integração com o Silverpop Engage
description: Saiba como integrar o Adobe Experience Manager ao Silverpop Engage.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Integração com o Silverpop Engage{#integrating-with-silverpop-engage}

<!-- THIS ENTIRE TOPIC APPEARS OBSOLETE BECAUSE SILVERPOP NO LONGER EXISTS AND THERE ARE NO REDIRECTS FOR THE DOWNLOAD URL BELOW THAT IS 404.
>[!NOTE]
>
>Silverpop integration is **not** available out of the box. Download the Silverpop integration package `https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content` from Package Share and install it on your instance. After you have installed the package, you can configure it as described in this document. -->

Integrar o AEM com o Silverpop Engage permite gerenciar e enviar emails criados no AEM por meio do Silverpop. Ele também permite usar os recursos de gerenciamento de clientes potenciais do Silverpop por meio de formulários AEM em páginas AEM.

A integração do oferece os seguintes recursos:

* A capacidade de criar emails no AEM e publicá-los no Silverpop para distribuição.
* A capacidade de definir a ação de um formulário AEM para criar um assinante do Silverpop.

Depois que o Silverpop Engage for configurado, você poderá publicar informativos ou emails no Silverpop Engage.

## Criação de uma configuração do Silverpop {#creating-a-silverpop-configuration}

As configurações do Silverpop podem ser adicionadas por meio de **Cloud Service**, **Ferramentas** ou **Pontos de extremidade da API**. Todos os métodos estão descritos nesta seção.

### Configuração do Silverpop por meio do Cloud Service {#configuring-silverpop-via-cloudservices}

Para criar uma configuração do Silverpop no Cloud Service:

1. No AEM, clique em **Ferramentas** > **Implantação** > **Cloud Service**. (Ou acesse diretamente em `https://<hostname>:<port>/etc/cloudservices.html`.)
1. Em serviços de terceiros, clique em **Silverop Engage** e depois **Configurar**. A janela de configuração do Silverpop é aberta.

   >[!NOTE]
   >
   >O Silverpop Engage não está disponível como uma opção em serviços de terceiros, a menos que você baixe o pacote do Compartilhamento de pacotes.

1. Insira um título e, opcionalmente, um nome e clique em **Criar**. A janela de configuração ** Silverpop Settings** (Configurações do Silverpop**) é aberta.
1. Insira o nome de usuário, a senha e selecione um endpoint da API na lista suspensa.
1. Clique em **Conecte-se ao Silverpop.** Depois de se conectar com êxito, você verá uma caixa de diálogo de sucesso. Clique em **OK** então você sai da janela. Você pode acessar o Silverpop clicando em **Ir para Silverpop Engage**.
1. O Silverpop foi configurado. Você pode editar a configuração clicando em **Editar**.
1. Além disso, a estrutura do Silverpop Engage pode ser configurada para ações personalizadas fornecendo título e nome (opcional). Clique em Criar com êxito para criar a estrutura da conexão do Silverpop já configurada.

   As colunas de extensão de dados importadas podem ser usadas posteriormente por meio do componente AEM - **Texto e personalização**.

### Configuração do Silverpop através de ferramentas {#configuring-silverpop-via-tools}

Para criar uma configuração do Silverpop em Ferramentas:

1. No AEM, clique em **Ferramentas** > **Implantação** > **Cloud Service**. Ou navegue até lá diretamente `https://<hostname>:<port>/misadmin#/etc`.
1. Selecionar **Ferramentas**, depois **Configurações do Cloud Service,** depois **Silverpop Engage**.
1. Clique em **Novo**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. No **Criar página** , insira o **Título** e, opcionalmente, a variável **Nome** e clique em **Criar**.
1. Insira as informações de configuração conforme descrito na etapa 4 do procedimento anterior. Siga esse procedimento para concluir a configuração do Silverpop.

### Adição de várias configurações {#adding-multiple-configurations}

Para adicionar várias configurações:

1. Na página de boas-vindas, clique em **Cloud Service** e clique em **Silverpop Engage**. Clique em **Exibir configurações** botão que aparece se uma ou mais configurações do Silverpop estiverem disponíveis. Todas as configurações disponíveis são listadas.
1. Clique em **+** faça logon ao lado de Configurações disponíveis. Ele abre o **Criar configurações** janela. Siga o procedimento de configuração anterior para criar uma configuração.

### Configuração de pontos de extremidade de API para conexão com o Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

Atualmente, o AEM tem seis pontos finais inseguros (Envolva 1 a 6). O Silverpop agora fornece dois novos pontos de extremidade e pontos de extremidade de conexão alterados para os existentes.

Para configurar os pontos de extremidade da API:

1. Ir para `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` em `https://<hostname>:<port>/crxde.`
1. Clique com o botão direito e selecione **Criar**, depois **Criar nó**.
1. Insira o **Nome** as `sp-e0` e escolha **Tipo** as `cq:Widget`.
1. Adicione duas propriedades ao nó recém-adicionado:

   1. **Nome**: `text`, **Tipo**: `String`, **Valor**: `Engage 0`
   1. **Nome**: `value`, **Tipo**: `String`, **Valor**: `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   Clique em &quot;Salvar tudo&quot;.

1. Criar mais um nó com **Nome** as `sp-e7` e **Tipo** as `cq:Widget`.

   Adicione duas propriedades ao nó recém-adicionado:

   1. **Nome**: `text`, **Tipo**: `String`, **Valor**: `Pilot`
   1. **Nome**: `value`, **Tipo**: `String`, **Valor**: `https://apipilot.silverpop.com/XMLAPI`

1. Para alterar os pontos de extremidade da API existentes (1 a 6), clique em cada um deles um por um e substitua os valores da seguinte maneira:

   | **Nome do nó** | **Valor do ponto de extremidade existente** | **Novo Valor de Ponto Final** |
   |---|---|---|
   | sp-e1 | `https://api.engage1.silverpop.com/XMLAPI` | `https://api1.silverpop.com` |
   | sp-e2 | `https://api.engage2.silverpop.com/XMLAPI` | `https://api2.silverpop.com` |
   | sp-e3 | `https://api.engage3.silverpop.com/XMLAPI` | `https://api3.silverpop.com` |
   | sp-e4 | `https://api.engage4.silverpop.com/XMLAPI` | `https://api4.silverpop.com` |
   | sp-e5 | `https://api.engage5.silverpop.com/XMLAPI` | `https://api5.silverpop.com` |
   | sp-e6 | `https://api.pilot.silverpop.com/XMLAPI` | `https://api6.silverpop.com` |

1. Clique em **Salvar tudo**. AEM agora está pronto para se conectar ao Silverpop sobre pontos finais seguros.

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
