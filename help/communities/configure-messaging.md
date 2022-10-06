---
title: Recurso Mensagens
seo-title: Messaging Feature
description: Configuração de componentes de mensagens
seo-description: Configuring Messaging components
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 4%

---

# Recurso Mensagens {#messaging-feature}

Além das interações publicamente visíveis que ocorrem em fóruns e comentários, o recurso de mensagens do AEM Communities permite que os membros da comunidade interajam mais privadamente.

Esse recurso pode ser incluído quando uma [site da comunidade](/help/communities/overview.md#communitiessites) é criada.

O recurso de mensagens oferece a capacidade de:

**A** - enviar uma mensagem para um ou mais membros da comunidade

**B** - enviar mensagens diretas em [em massa para grupos membros da comunidade](/help/communities/messaging.md#group-messaging)

**C** - enviar uma mensagem com anexos

**D** - encaminhar uma mensagem

**E** - responder a uma mensagem

**F** - excluir uma mensagem

**G** - restaurar uma mensagem excluída

![seção de mensagens](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

Para ativar e modificar o recurso de mensagens, consulte:

* [Configuração de mensagens](/help/communities/messaging.md) para administradores
* [Fundamentos das mensagens](/help/communities/essentials-messaging.md) para desenvolvedores

>[!NOTE]
>
>Não há suporte para adicionar `Compose Message, Message, or Message List` componentes (encontrados em `Communities`grupo de componentes) para uma página no modo de edição do autor.

## Configurar componentes de mensagens {#configure-messaging-components}

Quando as mensagens são ativadas para um site da comunidade, elas são configuradas sem necessidade de configuração adicional. As informações são fornecidas se houver a necessidade de alterar a configuração padrão.

### Configurar lista de mensagens (caixa de mensagem) {#configure-message-list-message-box}

Para modificar a configuração da lista de mensagens para **Caixa de entrada**, **Itens enviados** e **Lixeira** páginas do recurso de mensagens, abra o site em [modo de edição do autor](/help/communities/sites-console.md#authoring-site-content).

1. Em `Preview` selecione o **Mensagens** para abrir a página principal de mensagens. Em seguida, selecione **Caixa de entrada**, **Itens enviados** ou **Lixeira** para configurar o componente para a lista de mensagens.

1. Em `Edit` , selecione o componente na página.
1. Para acessar a caixa de diálogo de configuração, cancele a herança selecionando o `link` ícone .
Depois que a herança é cancelada, é possível selecionar o ícone de configuração para abrir a caixa de diálogo de configuração.

1. Quando a configuração for concluída, é necessário restaurar a herança selecionando a variável `broken link` ícone .

![configure-message-list](assets/configure-message-list.png)

#### Guia Básica {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Seletor de serviços**

   (*Obrigatório*) Defina isso como o valor da propriedade **`serviceSelector.name`** do [Serviço de operações de mensagens da AEM Communities](/help/communities/messaging.md#messaging-operations-service).

* **Compor página**

   (*Obrigatório*) A página a ser aberta quando um membro clicar no botão **`Reply`** botão. A página de destino deve conter a variável **Escrever mensagem** formulário.

* **Responder/Exibir como Recurso**

   Se marcada, o URL de resposta e o URL de exibição farão referência a um recurso, caso contrário, os dados serão passados como parâmetros de consulta no URL.

* **Formulário de exibição de perfil**

   O formulário de perfil a ser usado para exibir o perfil de remetentes.

* **Pasta Lixeira**

   Se marcada, esse componente Lista de mensagens exibe apenas mensagens sinalizadas como excluídas (lixeira).

* **Caminhos de pasta**

   (*Obrigatório*) Fazendo referência aos valores definidos para **inbox.path.name** e **sentitems.path.name** no [Serviço de operações de mensagens da AEM Communities](/help/communities/messaging.md#messaging-operations-service). Ao configurar para um `Inbox`, adicione uma entrada usando o valor de **inbox.path.name**. Ao configurar para um `Outbox`, adicione uma entrada usando o valor de **sentitems.path.name**. Ao configurar para `Trash`, adicione duas entradas com ambos os valores.

#### Guia Exibir {#display-tab}

![lista de mensagens com guias de exibição](assets/display-tab-message-list.png)

* **Botão Marcar Leitura**

   Se marcada, exibe uma `Read`que permite que uma mensagem seja marcada como lida.

* **Botão Marcar Não Lido**

   Se marcada, exibe uma `Mark Unread` que permite que uma mensagem seja marcada como lida.

* **Botão Excluir**

   Se marcada, exibe uma `Delete` que permite que uma mensagem seja marcada como lida. Duplicará a funcionalidade de exclusão se **`Message Options`** também está marcada.

* **Opções de mensagem**

   Se marcada, será exibida **`Reply`**, **`Reply All`**, **`Forward`** e **`Delete`** botões que permitem reenviar ou excluir uma mensagem. Duplicará a funcionalidade de exclusão se **`Delete Button`** também está marcada.

* **Mensagens por página**

   O número especificado é o número máximo de mensagens exibidas por página em um esquema de paginação. Se nenhum número for especificado (deixado em branco), todas as mensagens serão exibidas e não haverá paginação.

* **Padrões de data e hora**

   Forneça padrões de carimbo de data e hora para um ou mais idiomas. O padrão é en, de, fr, it, es, ja, zh_CN, ko_KR.

* **Exibir o usuário**

   Escolha um **`Sender`** ou **`Recipients`** para determinar se o Remetente ou o Recipients deve ser exibido.

### Configurar mensagem de composição {#configure-compose-message}

Para modificar a configuração da página de mensagens compostas, abra o site em [modo de edição do autor](/help/communities/sites-console.md#authoring-site-content).

* Em `Preview` selecione o **Mensagens** para abrir a página principal de mensagens. Em seguida, selecione o botão New Message para abrir o `Compose Message` página.

* Em `Edit` , selecione o componente principal na página que contém o corpo da mensagem.
* Para acessar a caixa de diálogo de configuração, cancele a herança selecionando o `link` ícone .
Depois que a herança é cancelada, é possível selecionar o ícone de configuração para abrir a caixa de diálogo de configuração.

* Quando a configuração for concluída, é necessário restaurar a herança selecionando a variável `broken link` ícone .

![config-compose-message](assets/config-compose-message.png)

#### Guia Básica {#basic-tab-1}

![composição básica de tabulação](assets/basic-tab-compose.png)

* **URI de redirecionamento**

   Insira o URL da página mostrada depois que a mensagem é enviada. Por exemplo, `../messaging.html`.

* **URL de cancelamento**

   Insira o URL da página mostrada se o remetente cancelar a mensagem. Por exemplo, `../messaging.html`.

* **Tamanho máximo do assunto da mensagem**

   O número máximo de caracteres permitidos no campo Assunto. Por exemplo, 500. O padrão não é limite.

* **Tamanho máximo do corpo da mensagem**

   O número máximo de caracteres permitidos no campo Conteúdo. Por exemplo, 10000. O padrão não é limite.

* **Seletor de serviços**

   (*Obrigatório*) Defina isso como o valor da propriedade **`serviceSelector.name`** do [Serviço de operações de mensagens da AEM Communities](/help/communities/messaging.md#messaging-operations-service).

#### Guia Exibir {#display-tab-1}

![exibir tabulação-compor](assets/display-tab-compose.png)

* **Mostrar campo de assunto**

   Se marcada, mostre a variável `Subject` e ativar a adição de um assunto à mensagem. O padrão não está marcado.

* **Rótulo do Assunto**

   Insira o texto a ser exibido ao lado do `Subject` campo. O padrão é `Subject`.

* **Mostrar campo Anexar arquivo**

   Se marcada, mostre a variável `Attachment` e habilite a adição de anexos de arquivo à mensagem. O padrão não está marcado.

* **Anexar etiqueta de arquivo**

   Insira o texto a ser exibido ao lado do `Attachment` campo. O padrão é **`Attach File`**.

* **Mostrar campo de conteúdo**

   Se marcada, mostre a variável `Content` e habilite a adição de um corpo de mensagem. O padrão não está marcado.

* **Rótulo de conteúdo**

   Insira o texto a ser exibido ao lado do `Content` campo. O padrão é **`Body`**.

* **Com Rich Text Editor**

   Se marcada, indica o uso de uma caixa de texto Conteúdo personalizada com seu próprio editor de rich text. O padrão não está marcado.

* **Padrões de data e hora**

   Forneça padrões de carimbo de data e hora para um ou mais idiomas. O padrão é en, de, fr, it, es, ja, zh_CN, ko_KR.
