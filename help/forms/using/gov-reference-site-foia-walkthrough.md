---
title: Apresentação do site de referência do We.Gov para a FOIA
seo-title: We.Gov reference site FOIA walkthrough
description: Consulte a apresentação do site de referência We.Gov para entender como a AEM Forms ajuda os governos a receber e transmitir as informações solicitadas por indivíduos de acordo com a Lei de Liberdade de Informação.
seo-description: See the We.Gov reference site walkthrough to understand how AEM Forms helps governments receive and impart information requested by individuals under the Freedom of Information Act.
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
exl-id: 57b5ce89-6b01-4087-a485-6d9696f06378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Apresentação do site de referência do We.Gov para a FOIA {#we-gov-reference-site-foia-walkthrough}

## Cenário do site de referência da Lei de liberdade de informações {#reference-site-freedom-of-information-act-scenario}

We.Gov é uma organização estatal que permite que os pais adotivos se inscrevam para receber pensão alimentícia se adotarem uma criança. We.Gov também permite que os pais solicitem informações dos seguintes departamentos do governo sob a lei de liberdade de informação:

* Agência de Logística da Defesa
* Departamento de Defesa Escritório do Inspetor Geral
* Departamento de Justiça - Escritório de Políticas de Informação
* Departamento da Marinha
* Agência de Proteção Ambiental

Para obter mais informações sobre a Lei de Liberdade de Informação, consulte [www.foia.gov](https://www.foia.gov).

O cenário envolve os seguintes perfis:

* Sarah Rose, a pessoa que solicita as informações
* John Jacobs, a pessoa que lida com a solicitação, a encaminha ao departamento apropriado
* Gloria Rios, a funcionária do governo que fornece as informações conforme o pedido

## Sarah inicia pedido de informações no âmbito da Foia {#sarah-initiates-request-for-information-under-foia}

De acordo com a Lei de Liberdade de Informação, Sarah solicita uma cópia dos registros de casos da Administração para Crianças e Famílias para o período de 2013 a 2016. Sarah apresenta este pedido ao Departamento de Justiça - Escritório de Política de Informação e também indica que está disposta a pagar até USD 100 para os custos de impressão e correio.

### Como funciona {#how-it-works}

### Veja você mesmo {#see-it-yourself}

No navegador, abra `https://<hostname>:<PublishPort>/wegov`. No site We.Gov, toque em Aplicativos > Todos os aplicativos. Na página Todos os aplicativos, toque em Aplicar em Aplicativo para solicitação FOIA.

## Sarah inicia seu pedido de informações sob a Foia {#sarah-starts-her-application-for-information-under-foia}

Cliques de Sarah **Aplicar** e na página Formulário de solicitação da Lei de liberdade de informações, Sarah insere informações, incluindo o seguinte:

* **Agência:** Sarah especifica a agência para a qual o pedido foi endereçado como Department of Justice - Office of Information Policy.

* **Pagará Até**: Sarah declara estar disposta a pagar até USD 100 por despesas de impressão e correio.
* **Descreva a solicitação em detalhes**: Sarah especifica &quot;Solicitando cópia dos registros de casos da Administração para crianças e famílias referentes aos anos fiscais de 2013 a 2016&quot;.

![Solicitando cópia dos registros de casos da Administração para Crianças e Famílias para os anos fiscais de 2013 a 2016](assets/sarahfiosform.png)

Solicitando cópia dos registros de casos da Administração para Crianças e Famílias para os anos fiscais de 2013 a 2016

A qualquer momento, Sarah pode tocar em Salvar para Salvar o rascunho do formulário e voltar mais tarde para preencher o formulário e enviá-lo. Sarah envia o formulário.

>[!NOTE]
>
>O fluxo de trabalho de retomada de email funciona somente com usuários conectados. No cenário do site de referência, verifique se Sarah Rose foi adicionada. As credenciais de login da Sarah são `srose/password`.

## John Jacobs recebe e aprova o aplicativo {#john-jacobs-receives-and-approves-the-application}

John Jacobs recebe as solicitações e as encaminha à pessoa certa. A caixa de entrada AEM permite que ela veja todas as solicitações de emprego enviadas em um único local.

### Como funciona {#how-it-works-1}

Quando Sarah preenche e envia o aplicativo FOIA, um registro do aplicativo é enviado para a caixa de entrada de John Jacobs. John Jacobs pode exibir a solicitação enviada e aceitá-la ou rejeitá-la.

### Veja você mesmo {#see-it-yourself-1}

Você pode acessar a caixa de entrada do AEM em https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Faça logon na caixa de entrada do AEM usando jacobs/password como nome de usuário/senha de John Jacobs e consulte o aplicativo FOIA. Para obter informações sobre como usar a Caixa de entrada AEM para tarefas de fluxo de trabalho centradas em formulários, consulte [Gerenciar aplicativos e tarefas do Forms na Caixa de entrada AEM](/help/forms/using/manage-applications-inbox.md).

![johnjacobs](assets/johnjacobs.png)

John Jacobs pode ver, aprovar ou rejeitar o aplicativo no painel de aplicativos. John Jacobs seleciona e abre os detalhes da solicitação e, após revisá-la, a aprova.

![johnjacobstaskdetail- 1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah recebe um email de confirmação</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

Depois que John Jacobs aprova o aplicativo, Sarah recebe um email de confirmação do site We.Gov. Sarah é informada sobre as taxas e o tempo necessário para o processamento de seu pedido. O e-mail também inclui detalhes de e-mail e telefone que Sarah pode contatar para obter atualizações sobre seu aplicativo.

![sarahroseemail](assets/sarahroseemail.png)

## Gloria recebe a solicitação da Foia para aprovação de segundo nível {#gloria-receives-the-foia-request-for-second-level-approval}

Depois que John Jacobs preenche as informações necessárias e aprova o pedido de Sarah, o pedido vai para Gloria Rios para a aprovação final. Gloria analisa o documento de registro anexo e aprova a solicitação.

![gloriariosinbox](assets/gloriariosinbox.png)

### Como funciona {#how-it-works-2}

Quando John Jacobs aprova o pedido FOIA, um PDF ou Documento de registro do aplicativo é criado e enviado para a caixa de entrada de Gloria Rios. Gloria pode visualizar a solicitação enviada e aprová-la ou rejeitá-la.

### Veja por si mesmo {#see-for-yourself}

Você pode acessar a caixa de entrada do AEM em https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Faça login na caixa de entrada do AEM usando grios/password como nome de usuário/senha de Gloria Rios e veja a solicitação de FOIS.

Gloria abre o pedido e examina os detalhes do pedido da Foia. Depois de rever os detalhes do pedido e verificar a viabilidade de fornecer os documentos requeridos, Gloria aprova o pedido.

![gloriariosapproes](assets/gloriariosapproves.png)

## Sarah recebe uma notificação de que seu pedido foi aprovado {#sarah-receives-notification-that-her-request-is-approved}

Depois que Gloria aprova o pedido da Foia, Sarah recebe um email notificando que seu pedido foi aprovado. O e-mail também inclui informações sobre o cronograma provisório para fornecer o documento e detalhes de contato para o acompanhamento da solicitação.

![sarahroseemailapproval](assets/sarahroseemailapproval.png)
