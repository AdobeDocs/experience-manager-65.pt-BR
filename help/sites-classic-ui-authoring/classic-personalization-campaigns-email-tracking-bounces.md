---
title: Rastreamento de emails devolvidos
description: Quando você envia um informativo para muitos usuários, geralmente há alguns endereços de email inválidos na lista. O envio de informativos para esses endereços será rejeitado. O AEM pode gerenciar essas rejeições e pode interromper o envio de informativos para esses endereços depois que o contador de rejeições configurado é excedido.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 6cda0a68-0df9-44e7-ae4f-9951411af6dd
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# Rastreamento de emails devolvidos{#tracking-bounced-emails}

>[!NOTE]
>
>O Adobe não planeja aprimorar ainda mais o rastreamento de emails abertos/rejeitados enviados pelo serviço AEM SMTP.
>
>A recomendação é [usar o Adobe Campaign e sua integração com o AEM](/help/sites-administering/campaign.md).

Quando você envia um informativo para muitos usuários, geralmente há alguns endereços de email inválidos na lista. O envio de informativos para esses endereços será rejeitado. O AEM pode gerenciar essas rejeições e pode interromper o envio de informativos para esses endereços depois que o contador de rejeições configurado é excedido. Por padrão, a taxa de rejeição é definida como 3, mas é configurável.

Para configurar o AEM para rastrear emails devolvidos, configure o AEM para pesquisar uma caixa de correio existente onde os emails devolvidos são recebidos. Normalmente, esse local é o endereço de email &quot;de&quot; que você especifica para onde enviar o informativo. O AEM pesquisa essa caixa de entrada e importa todos os emails abaixo do caminho especificado na configuração de pesquisa. Um fluxo de trabalho é acionado para procurar os endereços de email rejeitados nos usuários e atualiza o valor da propriedade bounceCounter do usuário de acordo. Depois que o máximo de rejeições configurado for excedido, o usuário será removido da lista de boletins informativos.

## Configuração do importador de feed {#configuring-the-feed-importer}

O importador de feed permite importar conteúdo repetidamente de fontes externas para o repositório. Com essa configuração do importador de feed, o AEM verifica se há emails devolvidos na caixa de correio do remetente.

Para configurar o importador de feed para rastrear emails devolvidos, faça o seguinte:

1. Em **Ferramentas**, selecione o Importador de Feed.

1. Clique em **Adicionar** para criar uma configuração.

   ![chlimage_1](assets/chlimage_1a.png)

1. Adicione uma configuração selecionando o tipo e adicionando informações ao URL de pesquisa para que você possa configurar o host e a porta. Além disso, adicione alguns parâmetros específicos de email e protocolo à consulta de URL. Defina a configuração para pesquisar pelo menos uma vez por dia.

   Todas as configurações precisam de informações sobre o seguinte no URL de pesquisa:

   `username`: O nome de usuário que é usado para conexão

   `password`: a senha usada para conexão

   Além disso, dependendo do protocolo, é possível definir determinadas configurações.

   **Propriedades de configuração POP3:**

   `pop3.leave.on.server`: Define se as mensagens devem ser deixadas no servidor ou não. Defina como verdadeiro para deixar mensagens no servidor; caso contrário, defina falso. O padrão é true.

   **Exemplos de POP3:**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | Usando pop3 sobre SSL para conectar ao GMail na porta 995 com usuário/segredo, deixando mensagens no servidor por padrão |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **Propriedades de configuração do IMAP:**

   Permite que você defina os sinalizadores a serem pesquisados.

   `imap.flag.SEEN`:Definir falso para mensagem nova/não vista, verdadeiro para mensagens já lidas

   Consulte [https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html](https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html) para obter a lista completa de sinalizadores.

   **Exemplos de IMAP:**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | Usando IMAP sobre SSL para conectar ao GMail na porta 993 com usuário/segredo. Recebendo novas mensagens somente por padrão. |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | Usando IMAP sobre SSL para conectar ao GMail 993 com usuário/segredo, obtendo apenas a mensagem já vista. |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | Usando IMAP sobre SSL para conectar ao GMail 993 com usuário/segredo, obtendo mensagens já lidas OU novas. |

1. Salve a configuração.

## Configuração do componente de serviço de boletim informativo {#configuring-the-newsletter-service-component}

Após configurar o importador de feed, configure o Endereço de origem e o contador de rejeição.

Para configurar o serviço de boletim informativo:

1. No console OSGi, em `<host>:<port>/system/console/configMgr`, navegue até o **Informativo MCM**.

1. Configure o serviço e salve as alterações ao concluir.

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   As seguintes configurações podem ser definidas para ajustar o comportamento:

   | Máximo do contador de rejeição (max.bounce.count) | Define o número de rejeições até que um usuário seja omitido ao enviar um informativo. Configurar esse valor como 0 desativa completamente a verificação de rejeição. |
   |---|---|
   | Atividade Sem Cache (sent.activity.nocache) | Define a configuração de cache a ser usada para a atividade de envio do informativo |

   Depois de salvo, o serviço MCM do boletim informativo faz o seguinte:

   * Grava uma atividade no fluxo oculto dos usuários ao enviar um boletim informativo com êxito.
   * Grava uma atividade se uma rejeição for detectada e o contador de rejeição do usuário for alterado.
