---
title: Gerenciar imagens de assinatura do agente
description: Depois de criar um modelo de correspondência, você pode usá-lo para criar correspondência no AEM Forms gerenciando dados, conteúdo e anexos.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: f044ed75-bb72-4be1-aef6-2fb3b2a2697b
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Gerenciar imagens de assinatura do agente{#manage-agent-signature-images}

## Visão geral {#overview}

No Gerenciamento de correspondências, você pode usar uma imagem para renderizar a assinatura do agente em cartas. Depois de configurar a imagem de assinatura do agente, ao criar uma correspondência, você pode renderizar a imagem de assinatura do agente na correspondência como a assinatura do agente remetente.

O DDE agentSignatureImage é um DDE calculado que representa a imagem de assinatura do agente. A expressão para esse DDE calculado usa uma nova função personalizada exposta pelo bloco de construção Gerenciador de Expressões. Essa função personalizada pega agentID e agentFolder como parâmetros de entrada e busca o conteúdo da imagem com base nesses parâmetros. O dicionário de dados do sistema SystemContext fornece cartas no Gerenciamento de correspondências com acesso a informações no contexto do sistema atual. O contexto do sistema inclui informações sobre o usuário conectado no momento e os parâmetros de configuração ativos.

Você pode adicionar imagens na pasta cmuserroot. Entrada [Propriedades de configuração do gerenciamento de correspondência](/help/forms/using/cm-configuration-properties.md), usando a propriedade Raiz de usuário do CM, é possível alterar a pasta da qual a imagem de assinatura do agente é recebida.

O valor de agentFolder DDE é retirado do parâmetro de configuração CMUserRoot para as propriedades de configuração do Gerenciamento de correspondência. Por padrão, esse parâmetro de configuração aponta para/content/cmUserRoot no repositório CRX. Você pode alterar o valor da configuração CMUserRoot nas Propriedades de configuração.
Também é possível substituir a função personalizada padrão para definir sua própria lógica de busca da imagem de assinatura do usuário.

## Adição da imagem de assinatura do agente {#adding-agent-signature-image}

1. Certifique-se de que a imagem de assinatura do agente tenha o mesmo nome do usuário AEM do usuário. (A extensão não é necessária para o nome de arquivo da imagem.)
1. No CRX, crie uma pasta chamada `cmUserRoot` na pasta de conteúdo.

   1. Ir para `https://'[server]:[port]'/crx/de`. Se necessário, efetue login como Administrador.

   1. Clique com o botão direito do mouse no **conteúdo** e selecione **Criar** > **Criar pasta**.

      ![Criar pasta](assets/1_createnode_cmuserroot.png)

   1. Na caixa de diálogo Criar pasta, digite o nome da pasta como `cmUserRoot`. Clique em **Salvar tudo**.

      >[!NOTE]
      >
      >cmUserRoot é o local padrão onde o AEM procura a imagem de assinatura do agente. No entanto, você pode alterá-la editando a propriedade Raiz de usuário do CM no [Propriedades de configuração do Gerenciamento de correspondência](/help/forms/using/cm-configuration-properties.md).

1. No Content Explorer, navegue até a pasta cmUserRoot e adicione a imagem de assinatura do agente nela.

   1. Ir para `https://'[server]:[port]'/crx/explorer/index.jsp`. Efetue login como Administrador, se necessário.
   1. Clique em **Content Explorer**. O Content Explorer é aberto em uma nova janela.
   1. No Content Explorer, navegue até a pasta cmUserRoot e selecione-a. Clique com o botão direito do mouse no **cmUserRoot** e selecione **Novo nó**.

      ![Novo nó em cmUserRoot](assets/2_cmuserroot_newnode.png)

      Faça as seguintes entradas na linha para o novo nó e clique na marca de seleção verde.

      **Nome:** JohnDoe (ou o nome do arquivo de assinatura do agente)

      **Tipo:** nt:arquivo

      No `cmUserRoot` pasta, uma nova pasta chamada `JohnDoe` (ou o nome fornecido na etapa anterior) é criado.

   1. Clique na nova pasta criada (aqui `JohnDoe`). O Content Explorer exibe o conteúdo da pasta como esmaecido.

   1. Clique duas vezes no ícone **jcr:content** propriedade, defina seu tipo como **nt:resource** e, em seguida, clique na marca de seleção verde para salvar a entrada.

      Se a propriedade não estiver presente, primeiro crie uma propriedade com o nome jcr:content.

      ![jcr:propriedade content](assets/3_jcrcontentntresource.png)

      Entre as subpropriedades de jcr:content está jcr:data, que está esmaecido. Clique duas vezes em jcr:data. A propriedade se torna editável e o botão Escolher arquivo aparece na entrada. Clique em **Escolher arquivo** e selecione o arquivo de imagem que deseja usar como logotipo. O arquivo de imagem não precisa ter uma extensão.

      ![Dados JCR](assets/5_jcrdata.png)

   Clique em **Salvar tudo**.

1. Certifique-se de que o XDP\layout usado na correspondência tenha um campo de imagem no canto inferior esquerdo (ou outro local apropriado no layout onde você deseja renderizar a assinatura) para renderizar a imagem da assinatura.
1. Ao criar a correspondência, na guia Dados, selecione um campo de imagem para a imagem de assinatura usando as seguintes etapas:

   1. Selecione Sistema no menu pop-up Tipo de vínculo, no painel direito.

   1. Selecione o DDE agentSignatureImage na lista do painel Elemento de dados para o DD SystemContext.

   1. Salve a carta.

1. Quando a correspondência é renderizada, você pode ver a assinatura na pré-visualização de correspondência no campo de imagem de acordo com o layout.

   ![Imagem de assinatura do agente na carta](assets/letterwithsignature.png)
