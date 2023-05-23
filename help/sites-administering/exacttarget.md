---
title: Integração com o ExactTarget
seo-title: Integrating with ExactTarget
description: Saiba como integrar o AEM ao ExactTarget.
seo-description: Learn how to integrate AEM with ExactTarget.
uuid: a53bbdaa-98f7-4035-b842-aa7ea63712ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5b2f624d-e5b8-4484-a773-7784ebce58bd
docset: aem65
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Integração com o ExactTarget{#integrating-with-exacttarget}

Integrar o AEM com o Exact Target permite gerenciar e enviar emails criados no AEM por meio do Exact Target. Ele também permite que você use os recursos de gerenciamento de clientes potenciais do Exact Target por meio de formulários AEM em páginas AEM.

A integração do oferece os seguintes recursos:

* A capacidade de criar emails no AEM e publicá-los no Exact Target para distribuição.
* A capacidade de definir a ação de um formulário AEM para criar um assinante do Exact Target.

Depois que o ExactTarget é configurado, você pode publicar informativos ou emails no ExactTarget. Consulte [Publicar informativos em um serviço de e-mail](/help/sites-authoring/personalization.md).

## Criação de uma configuração ExactTarget {#creating-an-exacttarget-configuration}

As configurações do ExactTarget podem ser adicionadas por meio de Cloud Services ou Ferramentas. Ambos os métodos são descritos nesta seção.

### Configuração do ExactTarget via Cloud Services {#configuring-exacttarget-via-cloudservices}

Para criar uma configuração ExactTarget em Cloud Services:

1. Na página de boas-vindas, clique em **Cloud Services**. (Ou acesse diretamente em `https://<hostname>:<port>/etc/cloudservices.html`.)
1. Clique em **ExactTarget** e depois **Configurar**. A janela de configuração ExactTarget é aberta.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Insira um título e, opcionalmente, um nome e clique em **Criar**. A variável **Configurações ExactTarget** é aberta.

   ![chlimage_1](assets/chlimage_1.jpeg)

1. Insira o nome de usuário, a senha e selecione um terminal de API (por exemplo, **https://webservice.exacttarget.com/Service.asmx**).
1. Clique em **Conectar ao ExactTarget.** Depois de se conectar com êxito, você verá uma caixa de diálogo de sucesso. Clique em **OK** para sair da janela.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Selecione uma conta, se disponível. A conta é para clientes do Enterprise 2.0. Clique em **OK**.

   O ExactTarget foi configurado. Você pode editar a configuração clicando em **Editar**. Você pode acessar o ExactTarget clicando em **Ir para ExactTarget**.

1. O AEM agora fornece um recurso de extensão de dados. Você pode importar colunas de extensão de dados ExactTarget. Ele pode ser configurado clicando no sinal &quot;+&quot; que aparece ao lado da configuração ExactTarget criada com sucesso. Qualquer extensão de dados existente pode ser selecionada na lista suspensa. Para obter mais informações sobre como configurar extensões de dados, consulte [Documentação do ExactTarget](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_relationships_classic.htm&amp;type=5).

   As colunas de extensão de dados importadas podem ser usadas posteriormente por meio do **Texto e personalização** componente.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### Configuração do ExactTarget via Ferramentas {#configuring-exacttarget-via-tools}

Para criar uma configuração ExactTarget em Ferramentas:

1. Na página de boas-vindas, clique em **Ferramentas**. Ou navegue até lá diretamente `https://<hostname>:<port>/misadmin#/etc`.
1. Selecionar **Ferramentas**, depois **Configurações do Cloud Services,** depois **ExactTarget**.
1. Clique em **Novo** para abrir a janela **Criar página**.

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. Insira o **Título** e, opcionalmente, a variável **Nome** e clique em **Criar**.
1. Insira as informações de configuração conforme descrito na etapa 4 do procedimento anterior. Siga esse procedimento para concluir a configuração do ExactTarget.

### Adição de várias configurações {#adding-multiple-configurations}

Para adicionar várias configurações:

1. Na página de boas-vindas, clique em **Cloud Services** e clique em **ExactTarget**. Clique em **Exibir configurações** botão que aparece se uma ou mais configurações ExactTarget estiverem disponíveis. Todas as configurações disponíveis são listadas.
1. Clique em **+** faça logon ao lado de Configurações disponíveis. Isso abre o **Criar configurações** janela. Siga o procedimento de configuração anterior para criar uma nova configuração.
