---
title: Recurso de mensagens
seo-title: Recurso de mensagens
description: Configuração de componentes de mensagens
seo-description: Configuração de componentes de mensagens
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Recurso de mensagens{#messaging-feature}

Além das interações publicamente visíveis que ocorrem em fóruns e comentários, o recurso de mensagens do **** AEM Communities permite que os membros da comunidade interajam mais privadamente.

Este recurso pode ser incluído quando um site [da](/help/communities/overview.md#communitiessites) comunidade é criado.

O recurso de mensagens oferece a capacidade de:

**A** - enviar uma mensagem para um ou mais membros **B** da comunidade - enviar mensagens diretas em [massa para grupos](/help/communities/messaging.md#group-messaging)**C** de membros da comunidade - enviar uma mensagem com anexos **D** - encaminhar uma mensagem**E - **resposta a uma mensagem **** F - eliminar uma mensagem**G ** - restaurar uma mensagem eliminada

![mensagem de](assets/messaging-section.png) restauração de seção ![de mensagens](assets/restore-message.png)

Para ativar e modificar o recurso de mensagens, consulte:

* [Configurar mensagens](/help/communities/messaging.md) para administradores
* [Princípios básicos](/help/communities/essentials-messaging.md) de mensagens para desenvolvedores

>[!NOTE]
>
>Não há suporte para adicionar `Compose Message, Message, or Message List` componentes (encontrados no grupo de `Communities`componentes) a uma página no modo de edição do autor.

## Configurar componentes de mensagens {#configure-messaging-components}

Quando as mensagens são ativadas para um site da comunidade, elas são configuradas sem necessidade de outras configurações. As informações são fornecidas se houver necessidade de alterar a configuração padrão.

### Configurar lista de mensagens (caixa de mensagem) {#configure-message-list-message-box}

Para modificar a configuração da lista de mensagens para **Caixa de entrada**, Itens **** enviados e **Lixeira **páginas do recurso de mensagem, abra o site no modo [de edição do](/help/communities/sites-console.md#authoring-site-content)autor.

1. No `Preview`modo, selecione o link **Mensagens **para abrir a página principal de mensagens. Em seguida, selecione **Caixa de entrada**, **Itens enviados **ou **Lixeira **para configurar o componente para a lista de mensagens.

1. No `Edit` modo, selecione o componente na página.
1. Para acessar a caixa de diálogo de configuração, cancele a herança selecionando o `link`ícone.
Após a herança ser cancelada, é possível selecionar o ícone de configuração para abrir a caixa de diálogo de configuração.

1. Quando a configuração for concluída, será necessário restaurar a herança selecionando o `broken link` ícone.

![configure-message-list](assets/configure-message-list.png)

#### Basic tab {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Seletor** de serviços (*obrigatório*) Defina como valor da propriedade**`serviceSelector.name`** do Serviço [de Operações de Mensagens do](/help/communities/messaging.md#messaging-operations-service)AEM Communities.

* **Compor página**(*obrigatório*) A página a ser aberta quando um membro clicar no botão **`Reply`**. A página de destino deve conter o formulário **Compor mensagem** .

* **Responder/Exibir como Recurso** Se marcada, o URL de resposta e o URL de exibição farão referência a um recurso, caso contrário, os dados serão transmitidos como parâmetros de consulta no URL.

* **Formulário** de exibição de perfilO formulário de perfil a ser usado para exibir o perfil dos remetentes.

* **Pasta** de lixeira Se marcada, esse componente Lista de mensagens exibirá somente as mensagens sinalizadas como excluídas (lixeira).

* **Caminhos** da pasta (*obrigatório*) Fazer referência aos valores definidos para **inbox.path.name** e **sentitems.path.name **no Serviço [de Operações de Mensagens do](/help/communities/messaging.md#messaging-operations-service)AEM Communities. Ao configurar para um `Inbox`, adicione uma entrada usando o valor de **inbox.path.name**. Ao configurar para um `Outbox`, adicione uma entrada usando o valor de **sentitems.path.name**. Ao configurar para `Trash`, adicione duas entradas com ambos os valores.

#### Guia Exibir {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **Botão** Marcar leitura Se marcada, exibe um `Read`botão que permite que uma mensagem seja marcada como lida.

* **Botão** Marcar não lido Se marcada, exibe um `Mark Unread` botão que permite que uma mensagem seja marcada como lida.

* **Botão Excluir** Se marcada, exibe um `Delete`botão que permite que uma mensagem seja marcada como lida. Duplicará a funcionalidade de exclusão se também **`Message Options`** estiver marcada.

* **Opções** de mensagem Se marcada, exibe **`Reply`**, **`Reply All`**, **`Forward`**e **`Delete`**botões permitindo que uma mensagem seja reenviada ou excluída. Duplicará a funcionalidade de exclusão se também **`Delete Button`** estiver marcada.

* **Mensagens por página** O número especificado é o número máximo de mensagens exibidas por página em um esquema de paginação. Se nenhum número for especificado (deixado em branco), todas as mensagens serão exibidas e não haverá paginação.

* **Padrões** de carimbo de data e hora Fornecem padrões de carimbo de data e hora para um ou mais idiomas. O padrão é en, de, fr, it, es, ja, zh_CN, ko_KR.

* **Exibir usuário** Escolha **`Sender`**`Recipients`ou ****para determinar se o remetente ou destinatário deve ser exibido.

### Configurar mensagem de composição {#configure-compose-message}

Para modificar a configuração da página de mensagem de composição, abra o site no modo [de edição do](/help/communities/sites-console.md#authoring-site-content)autor.

* No `Preview`modo, selecione o link **Mensagens **para abrir a página principal de mensagens. Em seguida, selecione o botão Nova mensagem para abrir a `Compose Message` página.

* No `Edit` modo, selecione o componente principal na página que contém o corpo da mensagem.
* Para acessar a caixa de diálogo de configuração, cancele a herança selecionando o `link`ícone.
Após a herança ser cancelada, é possível selecionar o ícone de configuração para abrir a caixa de diálogo de configuração.

* Quando a configuração for concluída, será necessário restaurar a herança selecionando o `broken link`ícone.

![config-compose-message](assets/config-compose-message.png)

#### Basic tab {#basic-tab-1}

![composição de guias básicas](assets/basic-tab-compose.png)

* **URL** de redirecionamentoInsira o URL da página exibida após o envio da mensagem. Por exemplo, `../messaging.html`.

* **Cancelar URL** Insira o URL da página exibida se o remetente cancelar a mensagem. Por exemplo, `../messaging.html`.

* **Tamanho máximo do assunto** da mensagem O número máximo de caracteres permitidos no campo Assunto. Por exemplo, 500. O padrão não é limite.

* **Comprimento máximo do corpo** da mensagem O número máximo de caracteres permitidos no campo Conteúdo. Por exemplo, 10000. O padrão não é limite.

* **Seletor** de serviços (*obrigatório*) Defina como valor da propriedade**`serviceSelector.name`** do Serviço [de Operações de Mensagens do](/help/communities/messaging.md#messaging-operations-service)AEM Communities.

#### Guia Exibir {#display-tab-1}

![composição de guias de exibição](assets/display-tab-compose.png)

* **Mostrar campo** de assunto Se marcado, mostre o `Subject` campo e ative a adição de um assunto à mensagem. O padrão não está marcado.

* **Rótulo** do assuntoInsira o texto a ser exibido ao lado do `Subject` campo. O padrão é `Subject`.

* **Mostrar campo** Anexar arquivo Se marcada, mostre o `Attachment` campo e ative a adição de anexos de arquivo à mensagem. O padrão não está marcado.

* **Anexar rótulo** do arquivoInsira o texto a ser exibido ao lado do `Attachment` campo. O padrão é **`Attach File`**.

* **Mostrar campo** de conteúdo Se marcada, mostre o `Content` campo e ative a adição de um corpo de mensagem. O padrão não está marcado.

* **Rótulo** do conteúdoInsira o texto a ser exibido ao lado do `Content` campo. O padrão é **`Body`**.

* **Com o Editor** de Rich Text Se marcada, indica o uso de uma caixa de texto Conteúdo personalizada com seu próprio editor de Rich Text. O padrão não está marcado.

* **Padrões** de carimbo de data e hora Fornecem padrões de carimbo de data e hora para um ou mais idiomas. O padrão é en, de, fr, it, es, ja, zh_CN, ko_KR.

