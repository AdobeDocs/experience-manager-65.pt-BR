---
title: Integração com o ExactTarget
seo-title: Integração com o ExactTarget
description: Saiba como integrar o AEM ao ExactTarget.
seo-description: Saiba como integrar o AEM ao ExactTarget.
uuid: a53bbdaa-98f7-4035-b842-aa7ea63712ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5b2f624d-e5b8-4484-a773-7784ebce58bd
docset: aem65
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2

---


# Integração com o ExactTarget{#integrating-with-exacttarget}

Integrar o AEM ao Target exato permite gerenciar e enviar emails criados no AEM por meio do Target exato. Também permite que você use os recursos de gerenciamento de lead do Target Exata por meio de formulários AEM em páginas AEM.

A integração oferece os seguintes recursos:

* A capacidade de criar e-mails no AEM e publicá-los no Target exato para distribuição.
* A capacidade de definir uma ação de um formulário AEM para criar um assinante Exato do Target.

Depois que o ExactTarget for configurado, você poderá publicar boletins informativos ou emails no ExactTarget. Consulte [Publicar Newsletters em um serviço](/help/sites-authoring/personalization.md)de email.

## Criando uma configuração ExactTarget {#creating-an-exacttarget-configuration}

As configurações ExactTarget podem ser adicionadas por meio dos serviços Cloudservices ou das Ferramentas. Ambos os métodos estão descritos nesta seção.

### Configuração do ExactTarget via Cloudservices {#configuring-exacttarget-via-cloudservices}

Para criar uma configuração ExactTarget nos Serviços em nuvem:

1. Na página de boas-vindas, clique em Serviços **da** nuvem. (Ou acesso direto em `https://<hostname>:<port>/etc/cloudservices.html`.)
1. Clique em **ExactTarget** e em **Configurar**. A janela de configuração ExactTarget é aberta.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Enter a title and optionally, a name and click **Create**. A janela de configuração **ExactTarget Settings** é aberta.

   ![chlimage_1](assets/chlimage_1.jpeg)

1. Digite o nome de usuário, a senha e selecione um terminal de API (por exemplo, **https://webservice.exacttarget.com/Service.asmx**).
1. Clique em **Conectar-se ao ExactTarget.** Quando você se conectou com êxito, verá uma caixa de diálogo de sucesso. Clique em **OK** para sair da janela.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Selecione uma conta, se disponível. A conta é para clientes do Enterprise 2.0. Clique em **OK**.

   ExactTarget foi configurado. Você pode editar a configuração clicando em **Editar**. Você pode acessar ExactTarget clicando em **Ir para ExactTarget**.

1. O AEM agora fornece um recurso de Extensão de dados. É possível importar colunas de extensão de dados ExactTarget. Isso pode ser configurado clicando no sinal &quot;+&quot; que aparece além de ter criado com êxito a configuração ExactTarget. Qualquer extensão de dados existente pode ser selecionada na lista suspensa. Para obter mais informações sobre como configurar extensões de dados, consulte a documentação do [ExactTarget](https://help.exacttarget.com/en/documentation/exacttarget/subscribers/data_extensions_and_data_relationships).

   Colunas de extensão de dados importadas podem ser usadas posteriormente por meio do componente **Texto e Personalização** .

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### Configuração do ExactTarget via Ferramentas {#configuring-exacttarget-via-tools}

Para criar uma configuração ExactTarget em Ferramentas:

1. Na página de boas-vindas, clique em **Ferramentas**. Ou navegue lá diretamente indo para `https://<hostname>:<port>/misadmin#/etc`.
1. Selecione **Ferramentas**, Configurações de serviços **em nuvem,** em seguida, **ExactTarget**.
1. Click **New** to open the **Create Page **window.

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. Enter the **Title** and optionally the **Name**, and click **Create**.
1. Digite as informações de configuração conforme descrito na etapa 4 do procedimento anterior. Siga esse procedimento para concluir a configuração do ExactTarget.

### Adicionar várias configurações {#adding-multiple-configurations}

Para adicionar várias configurações:

1. Na página de boas-vindas, clique em Serviços **da** nuvem e em **ExactTarget**. Clique no botão **Mostrar configurações** que será exibido se uma ou mais configurações ExactTarget estiverem disponíveis. Todas as configurações disponíveis são listadas.
1. Clique no sinal **+** ao lado de Configurações disponíveis. Isso abre a janela **Criar configurações** . Siga o procedimento de configuração anterior para criar uma nova configuração.