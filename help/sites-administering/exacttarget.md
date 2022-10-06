---
title: Integração com o ExactTarget
seo-title: Integrating with ExactTarget
description: Saiba como integrar o AEM com o ExactTarget.
seo-description: Learn how to integrate AEM with ExactTarget.
uuid: a53bbdaa-98f7-4035-b842-aa7ea63712ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5b2f624d-e5b8-4484-a773-7784ebce58bd
docset: aem65
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Integração com o ExactTarget{#integrating-with-exacttarget}

Integrar AEM com o Exact Target permite gerenciar e enviar emails criados no AEM por meio do Exact Target. Também permite usar os recursos de gerenciamento de clientes potenciais do Exact Target por meio de formulários AEM em páginas AEM.

A integração oferece os seguintes recursos:

* A capacidade de criar emails no AEM e publicá-los no Exact Target para distribuição.
* A capacidade de definir uma ação de um formulário AEM para criar um assinante Exato do Target.

Depois que o ExactTarget é configurado, você pode publicar informativos ou emails no ExactTarget. Consulte [Publicar informativos em um serviço de email](/help/sites-authoring/personalization.md).

## Criação de uma configuração ExactTarget {#creating-an-exacttarget-configuration}

As configurações ExactTarget podem ser adicionadas por meio de Cloudservices ou Ferramentas. Ambos os métodos estão descritos nesta seção.

### Configuração do ExactTarget via Cloudservices {#configuring-exacttarget-via-cloudservices}

Para criar uma configuração ExactTarget no Cloud Services:

1. Na página de boas-vindas, clique em **Cloud Services**. (Ou acesse diretamente em `https://<hostname>:<port>/etc/cloudservices.html`.)
1. Clique em **ExactTarget** e depois **Configurar**. A janela de configuração ExactTarget é aberta.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Insira um título e, opcionalmente, um nome e clique em **Criar**. O **Configurações do ExactTarget** janela de configuração é aberta.

   ![chlimage_1](assets/chlimage_1.jpeg)

1. Digite o nome de usuário, a senha e selecione um ponto de extremidade de API (por exemplo, **https://webservice.exacttarget.com/Service.asmx**).
1. Clique em **Conecte-se ao ExactTarget.** Depois de se conectar com êxito, você verá uma caixa de diálogo de sucesso. Clique em **OK** para sair da janela.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Selecione uma conta, se disponível. A conta é para clientes do Enterprise 2.0. Clique em **OK**.

   O ExactTarget foi configurado. Você pode editar a configuração clicando em **Editar**. Você pode acessar o ExactTarget clicando em **Ir para ExactTarget**.

1. AEM agora fornece um recurso de Extensão de dados. É possível importar colunas de extensão de dados do ExactTarget. Isso pode ser configurado clicando no sinal &quot;+&quot; que aparece além da configuração ExactTarget criada com êxito. Qualquer extensão de dados existente pode ser selecionada na lista suspensa. Para obter mais informações sobre como configurar extensões de dados, consulte [Documentação do ExactTarget](https://help.exacttarget.com/en/documentation/exacttarget/subscribers/data_extensions_and_data_relationships).

   Colunas de extensão de dados importadas podem ser usadas posteriormente por meio do **Texto e personalização** componente.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### Configuração do ExactTarget via Ferramentas {#configuring-exacttarget-via-tools}

Para criar uma configuração ExactTarget em Ferramentas:

1. Na página de boas-vindas, clique em **Ferramentas**. Ou navegue diretamente lá, indo até `https://<hostname>:<port>/misadmin#/etc`.
1. Selecionar **Ferramentas**, em seguida **Configurações Cloud Services,** then **ExactTarget**.
1. Clique em **Novo** para abrir a janela **Criar página **i.

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. Insira o **Título** e, opcionalmente, **Nome** e clique em **Criar**.
1. Insira as informações de configuração conforme descrito na etapa 4 do procedimento anterior. Siga esse procedimento para concluir a configuração do ExactTarget.

### Adição de várias configurações {#adding-multiple-configurations}

Para adicionar várias configurações:

1. Na página de boas-vindas, clique em **Cloud Services** e clique em **ExactTarget**. Clique em **Mostrar configurações** que é exibido se uma ou mais configurações ExactTarget estiverem disponíveis. Todas as configurações disponíveis são listadas.
1. Clique no botão **+** assine ao lado de Configurações disponíveis. Isso abre o **Criar configurações** janela. Siga o procedimento de configuração anterior para criar uma nova configuração.
