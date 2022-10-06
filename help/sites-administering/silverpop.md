---
title: Integração com o Silverpop Engage
seo-title: Integrating with Silverpop Engage
description: Saiba como integrar o AEM com o Silverpop Engage
seo-description: Learn how to integrate AEM with Silverpop Engage
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# Integração com o Silverpop Engage{#integrating-with-silverpop-engage}

>[!NOTE]
>
>A integração do Silverpop é **not** disponível imediatamente. Você deve baixar o [Pacote de integração do Silverpop](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content) do Compartilhamento de pacotes e instale-o em sua instância. Depois de instalar o pacote, você pode configurá-lo conforme descrito neste documento.

Integrar AEM com o Silverpop Engage permite gerenciar e enviar emails criados no AEM via Silverpop. Também permite usar os recursos de gerenciamento de clientes potenciais do Silverpop por meio de formulários AEM em páginas AEM.

A integração oferece os seguintes recursos:

* A capacidade de criar emails no AEM e publicá-los no Silverpop para distribuição.
* A capacidade de definir uma ação de um formulário AEM para criar um assinante do Silverpop.

Depois que o Silverpop Engage é configurado, você pode publicar informativos ou emails no Silverpop Engage.

## Criação de uma configuração do Silverpop {#creating-a-silverpop-configuration}

As configurações do Silverpop podem ser adicionadas por meio de **Serviços de nuvem**, **Ferramentas** ou **Pontos finais da API**. Todos os métodos estão descritos nesta seção.

### Configuração do Silverpop via Cloudservices {#configuring-silverpop-via-cloudservices}

Para criar uma configuração do Silverpop no Cloud Services:

1. Em AEM, toque ou clique em **Ferramentas** > **Implantação** > **Cloud Services**. (Ou acesse diretamente em `https://<hostname>:<port>/etc/cloudservices.html`.)
1. Em serviços de terceiros, clique em **Silverop Engage** e depois **Configurar**. A janela de configuração do Silverpop é aberta.

   >[!NOTE]
   >
   >O Silverpop Engage não está disponível como uma opção em serviços de terceiros, a menos que você baixe o pacote do Compartilhamento de pacotes.

1. Insira um título e, opcionalmente, um nome e clique em **Criar**. A janela de configuração** Silverpop Settings** é aberta.
1. Digite o nome de usuário, a senha e selecione um endpoint da API na lista suspensa.
1. Clique em **Conecte-se ao Silverpop.** Depois de se conectar com êxito, você verá uma caixa de diálogo de sucesso. Clique em **OK** para sair da janela. Você pode acessar o Silverpop clicando em **Ir para o Silverpop Engage**.
1. O Silverpop foi configurado. Você pode editar a configuração clicando em **Editar**.
1. Além disso, a estrutura do Silverpop Engage pode ser configurada para ações personalizadas fornecendo título e nome (opcional). Clique em Criar para criar a estrutura para a conexão Silverpop já configurada.

   Colunas de extensão de dados importadas podem ser usadas posteriormente por meio do componente AEM - **Texto e personalização**.

### Configuração do Silverpop por meio de ferramentas {#configuring-silverpop-via-tools}

Para criar uma configuração do Silverpop em Ferramentas:

1. Em AEM, toque ou clique em **Ferramentas** > **Implantação** > **Cloud Services**. Ou navegue diretamente lá, indo até `https://<hostname>:<port>/misadmin#/etc`.
1. Selecionar **Ferramentas**, em seguida **Configurações Cloud Services,** then **Silverpop Engage**.
1. Clique em **Novo** para abrir a janela **Criar página**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. Insira o **Título** e, opcionalmente, **Nome** e clique em **Criar**.
1. Insira as informações de configuração conforme descrito na etapa 4 do procedimento anterior. Siga esse procedimento para concluir a configuração do Silverpop.

### Adição de várias configurações {#adding-multiple-configurations}

Para adicionar várias configurações:

1. Na página de boas-vindas, clique em **Cloud Services** e clique em **Silverpop Engage**. Clique em **Mostrar configurações** botão que é exibido se uma ou mais configurações do Silverpop estiverem disponíveis. Todas as configurações disponíveis são listadas.
1. Clique no botão **+** assine ao lado de Configurações disponíveis. Isso abre o **Criar configurações** janela. Siga o procedimento de configuração anterior para criar uma nova configuração.

### Configuração de pontos de extremidade de API para conexão com o Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

Atualmente, AEM tem seis pontos finais não seguros (Envolvimento de 1 a 6). O Silverpop agora fornece dois novos pontos finais, bem como pontos finais de conexão alterados para os existentes.

Para configurar os pontos finais da API:

1. Ir para `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` on `https://<hostname>:<port>/crxde.`
1. Clique com o botão direito do mouse e selecione **Criar**, em seguida **Criar nó**.
1. Insira o **Nome** as `sp-e0` e escolha **Tipo** as `cq:Widget`.
1. Adicione duas propriedades ao nó recém-adicionado:

   1. **Nome**: `text`, **Tipo**: `String`, **Valor**: `Engage 0`
   1. **Nome**: `value`, **Tipo**: `String`, **Valor**: `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   Clique no botão &quot;Salvar tudo&quot;.

1. Crie mais um nó com **Nome** as `sp-e7` e **Tipo** as `cq:Widget`.

   Adicione duas propriedades ao nó recém-adicionado:

   1. **Nome**: `text`, **Tipo**: `String`, **Valor**: `Pilot`
   1. **Nome**: `value`, **Tipo**: `String`, **Valor**: `https://apipilot.silverpop.com/XMLAPI`

1. Para alterar os Pontos de extremidade da API existentes (Envolva 1 a 6), clique em cada um deles um por um e substitua os valores da seguinte maneira:

   | **Nome do nó** | **Valor do Ponto Final Existente** | **Novo Valor de Ponto Final** |
   |---|---|---|
   | sp-e1 | https://api.engage1.silverpop.com/XMLAPI | https://api1.silverpop.com |
   | sp-e2 | https://api.engage2.silverpop.com/XMLAPI | https://api2.silverpop.com |
   | sp-e3 | https://api.engage3.silverpop.com/XMLAPI | https://api3.silverpop.com |
   | sp-e4 | https://api.engage4.silverpop.com/XMLAPI | https://api4.silverpop.com |
   | sp-e5 | https://api.engage5.silverpop.com/XMLAPI | https://api5.silverpop.com |
   | sp-e6 | https://api.pilot.silverpop.com/XMLAPI | https://api6.silverpop.com |

1. Clique em **Salvar tudo**. AEM agora está pronto para se conectar ao Silverpop em pontos de extremidade protegidos.

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
