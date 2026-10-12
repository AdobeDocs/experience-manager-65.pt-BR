---
title: Integração com o ExactTarget
description: Saiba como integrar o Adobe Experience Manager ao ExactTarget.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%
---
# Integração com o ExactTarget{#integrating-with-exacttarget}

A integração do Adobe Experience Manager (AEM) com o Exact Target permite gerenciar e enviar emails criados no AEM por meio do Exact Target. Ele também permite usar os recursos de gerenciamento de clientes potenciais do Exact Target por meio de formulários do AEM em páginas do AEM.

A integração do oferece os seguintes recursos:

* A capacidade de criar emails no AEM e publicá-los no Exact Target para distribuição.
* A capacidade de definir a ação de um formulário do AEM para criar um assinante do Exact Target.

Depois que o ExactTarget é configurado, você pode publicar informativos ou emails no ExactTarget. Consulte [Publicar informativos em um serviço de email](/help/sites-authoring/personalization.md).

## Criação de uma configuração ExactTarget {#creating-an-exacttarget-configuration}

As configurações do ExactTarget podem ser adicionadas por meio do Cloud Services ou das Ferramentas. Ambos os métodos são descritos nesta seção.

### Configuração do ExactTarget por meio dos serviços em nuvem {#configuring-exacttarget-via-cloudservices}

Para criar uma configuração ExactTarget no Cloud Services:

1. Na página de boas-vindas, clique em **Cloud Services**. (Ou acesse diretamente em `https://<hostname>:<port>/etc/cloudservices.html`.)
1. Clique em **ExactTarget** e depois em **Configurar**. A janela de configuração ExactTarget é aberta.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Insira um título, opcionalmente um nome e clique em **Criar**. A janela de configuração **Configurações ExactTarget** é aberta.

   ![chlimage_1](assets/chlimage_1.jpeg)

1. Insira o nome de usuário, a senha e selecione um ponto de extremidade de API (por exemplo, **https://webservice.exacttarget.com/Service.asmx**).
1. Clique em **Conectar ao ExactTarget.** Depois de se conectar com êxito, você verá uma caixa de diálogo de sucesso. caixa Clique em **OK** para sair da janela.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Selecione uma conta, se disponível. A conta é para clientes do Enterprise 2.0. Clique em **OK**.

   O ExactTarget foi configurado. Você pode editar a configuração clicando em **Editar**. Você pode ir para ExactTarget clicando em **Ir para ExactTarget**.

1. O AEM agora fornece um recurso de extensão de dados. Você pode importar colunas de extensão de dados ExactTarget. Ele pode ser configurado clicando no sinal &quot;+&quot; que aparece ao lado da configuração ExactTarget criada com sucesso. Qualquer extensão de dados existente pode ser selecionada na lista suspensa. Para obter mais informações sobre como configurar extensões de dados, consulte a [documentação do ExactTarget](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_relationships_classic.htm&type=5).

   Colunas de extensão de dados importadas podem ser usadas posteriormente por meio do componente **Text e Personalization**.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### Configuração do ExactTarget por meio das Ferramentas {#configuring-exacttarget-via-tools}

Para criar uma configuração ExactTarget em Ferramentas:

1. Na página de boas-vindas, clique em **Ferramentas**. Ou navegue diretamente até `https://<hostname>:<port>/misadmin#/etc`.
1. Selecione **Ferramentas**, depois **Configurações de Cloud Services** e depois **ExactTarget**.
1. Clique em **Novo** para abrir a janela **Criar página**.

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. Insira o **Título** e, opcionalmente, o **Nome** e clique em **Criar**.
1. Insira as informações de configuração conforme descrito na etapa 4 do procedimento anterior. Siga esse procedimento para concluir a configuração do ExactTarget.

### Adição de várias configurações {#adding-multiple-configurations}

Para adicionar várias configurações:

1. Na página de boas-vindas, clique em **Cloud Services** e em **ExactTarget**. Clique em **Mostrar Configurações**, que aparecerá se uma ou mais configurações do ExactTarget estiverem disponíveis. Todas as configurações disponíveis são listadas.
1. Clique no sinal **+** ao lado de Configurações disponíveis. Isso abre a janela **Criar Configurações**. Siga o procedimento de configuração anterior para criar uma configuração.
