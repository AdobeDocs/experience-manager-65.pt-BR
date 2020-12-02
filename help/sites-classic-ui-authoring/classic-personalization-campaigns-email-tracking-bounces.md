---
title: Rastreamento de emails retornados
seo-title: Rastreamento de emails retornados
description: Quando você envia um informativo para muitos usuários, geralmente há alguns endereços de email inválidos na lista. O envio de informativos para esses endereços é devolvido. O AEM é capaz de gerenciar esses saltos e pode parar de enviar informativos para esses endereços depois que o contador de saltos configurado for excedido.
seo-description: Quando você envia um informativo para muitos usuários, geralmente há alguns endereços de email inválidos na lista. O envio de informativos para esses endereços é devolvido. O AEM é capaz de gerenciar esses saltos e pode parar de enviar informativos para esses endereços depois que o contador de saltos configurado for excedido.
uuid: 749959f2-e6f8-465f-9675-132464c65f11
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: fde9027b-9057-48c3-ae34-3f3258c5b371
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 63%

---


# Rastreamento de emails retornados{#tracking-bounced-emails}

>[!NOTE]
>
>O Adobe não pretende melhorar ainda mais o rastreamento de emails abertos/enviados por AEM serviço SMTP.
>
>A recomendação é [aproveitar a Adobe Campaign e sua integração AEM](/help/sites-administering/campaign.md).

Quando você envia um informativo para muitos usuários, geralmente há alguns endereços de email inválidos na lista. O envio de informativos para esses endereços é devolvido. O AEM é capaz de gerenciar esses saltos e pode parar de enviar informativos para esses endereços depois que o contador de saltos configurado for excedido. Por padrão, a taxa de saltos é definida como 3, mas pode ser configurada.

Para configurar o AEM para rastrear emails devolvidos, é necessário configurar o AEM para pesquisar uma caixa de correio existente na qual os emails devolvidos são recebidos (geralmente, esse é o endereço de email &quot;De&quot; que você especifica para enviar o informativo). O AEM pesquisa essa caixa de entrada e importa todos os emails abaixo do caminho especificado na configuração de pesquisa. Um fluxo de trabalho é acionado para pesquisar os endereços de email enviados dentro dos usuários e atualiza o valor da propriedade bounceCounter do usuário de acordo. Após os saltos máximos configurados serem excedidos, o usuário é removido da lista de informativos.

## Configuração do importador de feeds {#configuring-the-feed-importer}

O importador de feeds permite que você importe repetidamente conteúdo de fontes externas para o seu repositório. Com essa configuração do importador de feed, o AEM verifica a caixa de correio do remetente em busca de emails devolvidos.

Para configurar o importador de feeds para rastrear emails devolvidos:

1. Em **Ferramentas**, selecione o Importador de feed.

1. Clique em **Adicionar** para criar uma nova configuração.

   ![chlimage_1](assets/chlimage_1a.png)

1. Adicione uma nova configuração selecionando o tipo e acrescentando informações ao URL de pesquisa para configurar o host e a porta. Além disso, você precisa adicionar alguns parâmetros específicos de email e protocolo à consulta de URL. Defina a configuração para pesquisar pelo menos uma vez por dia.

   Todas as configurações precisam de informações sobre o seguinte no URL de pesquisa:

   `username`: O nome de usuário a ser usado para conexão

   `password`: A senha a ser usada para conexão

   Além disso, dependendo do protocolo, você pode definir certas configurações.

   **Propriedades de configuração POP3:**

   `pop3.leave.on.server`: Define se as mensagens devem ou não ser deixadas no servidor. Defina como true para deixar mensagens no servidor, caso contrário, defina como false. O padrão é true.

   **Exemplos de POP3:**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | Usar pop3 sobre SSL para conectar-se ao GMail na porta 995 com usuário/segredo, deixando mensagens no servidor por padrão |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **Propriedades de configuração IMAP:**

   Permite que você defina sinalizadores para procurar.

   `imap.flag.SEEN`:Definir false para mensagem nova/não vista, true para mensagens já lidas

   Consulte [https://java.sun.com/products/javamail/javadocs/javax/mail/Flags.Flag.html](https://java.sun.com/products/javamail/javadocs/javax/mail/Flags.Flag.html) para obter a lista completa de sinalizadores.

   **Exemplos de IMAP:**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | Usar o IMAP sobre SSL para conectar-se ao GMail na porta 993 com usuário/segredo. Por padrão, apenas obtendo novas mensagens. |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | Usar o IMAP sobre SSL para conectar-se ao GMail 993 com usuário/segredo, apenas recebendo uma mensagem já vista. |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | Usar o IMAP sobre SSL para conectar-se ao GMail 993 com usuário/segredo, já lendo OU novas mensagens. |

1. Salve a configuração.

## Configuração do componente de serviço de informativo {#configuring-the-newsletter-service-component}

Depois de configurar o importador de feeds, você precisa configurar o endereço De e o contador de saltos.

Para configurar o serviço de informativo:

1. No console OSGi em `<host>:<port>/system/console/configMgr` e navegue até **Newsletter MCM**.

1. Configure o serviço e salve as alterações quando terminar.

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   As seguintes configurações podem ser definidas para ajustar o comportamento:

   | Contador de rejeição máximo (max.bounce.count) | Define o número de rejeições até que um usuário seja omitido ao enviar um boletim informativo. Definir este valor como 0 desativa completamente a verificação de saltos. |
   |---|---|
   | Atividade sem cache (send.atividade.nocache) | Define a configuração de cache a ser usada para a atividade enviada para o boletim informativo |

   Depois de salvo, o serviço MCM do informativo faz o seguinte:

   * Grava uma atividade no fluxo ocultos de usuários após o envio bem-sucedido de um informativo.
   * Grava uma atividade se um salto for detectado, e o contador de saltos dos usuários é alterada.
