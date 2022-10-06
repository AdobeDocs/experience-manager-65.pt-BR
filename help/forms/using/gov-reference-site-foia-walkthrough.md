---
title: Apresentação do site de referência do We.Gov FOIA
seo-title: We.Gov reference site FOIA walkthrough
description: Consulte a apresentação do site de referência We.Gov para entender como a AEM Forms ajuda os governos a receber e entregar informações solicitadas por indivíduos sob a Lei de Liberdade de Informação.
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

# Apresentação do site de referência do We.Gov FOIA {#we-gov-reference-site-foia-walkthrough}

## Cenário da Lei de Liberdade de Informação do site de referência {#reference-site-freedom-of-information-act-scenario}

We.Gov é uma organização estatal que permite que pais adotivos se inscrevam para receber apoio infantil caso tenham adotado uma criança. We.Gov também permite que os pais solicitem informações aos seguintes departamentos do governo sob a lei de liberdade de informação:

* Agência de Logística da Defesa
* Departamento de Defesa do Serviço de Inspetores-Geral
* Departamento de Justiça - Gabinete da Política de Informação
* Departamento da Marinha
* Agência de Proteção do Ambiente

Para obter mais informações sobre a Lei de Liberdade de Informação, consulte [www.foia.gov](https://www.foia.gov).

O cenário envolve as seguintes personas:

* Sarah Rose, a pessoa que pede informações sob
* John Jacobs, a pessoa que trata do pedido, o encaminha para o departamento adequado
* Gloria Rios, funcionária do governo que fornece as informações conforme o pedido

## Sarah dá início a um pedido de informações ao abrigo da FOIA {#sarah-initiates-request-for-information-under-foia}

De acordo com a Lei de Liberdade de Informação, Sarah solicita uma cópia dos registros de processos da Administração para Crianças e Famílias por anos (AF) 2013 até 2016. Sarah submete este pedido ao Departamento de Justiça - Gabinete de Política de Informação e também significa que está disposta a pagar até 100 dólares pelos custos de impressão e de envio.

### Como funciona {#how-it-works}

### Veja você mesmo {#see-it-yourself}

No seu navegador, abra `https://<hostname>:<PublishPort>/wegov`. No site We.Gov, toque em Aplicativos > Todos os aplicativos. Na página Todos os aplicativos , toque em Aplicar, em Aplicativo para solicitação FOIA.

## Sarah dá início a seu pedido de informação no FOIA {#sarah-starts-her-application-for-information-under-foia}

Sarah clica **Aplicar** e na página Formulário de solicitação da Lei de Liberdade de Informação, Sarah insere informações incluindo o seguinte:

* **Agência:** Sarah especifica a agência para a qual o pedido foi endereçado como Departamento de Justiça - Escritório de Política de Informação.

* **Pagará Até**: Sarah especifica que está disposta a pagar até 100 dólares para as despesas de impressão e correio.
* **Descreva a solicitação em detalhes**: Sarah especifica &quot;Solicitando cópia dos registros de caso da Administração para Crianças e Famílias para os anos fiscais de 2013 até 2016&quot;.

![Solicitação de cópia dos registros de caso da Administração para Crianças e Famílias para os anos fiscais de 2013 até 2016](assets/sarahfiosform.png)

Solicitação de cópia dos registros de caso da Administração para Crianças e Famílias para os anos fiscais de 2013 até 2016

A qualquer momento, Sarah pode tocar em Salvar para Salvar o rascunho do formulário e retornar posteriormente para preencher o formulário e enviá-lo. Sarah submete o formulário.

>[!NOTE]
>
>O fluxo de trabalho resume-from-email funciona somente com usuários conectados. Na situação do site de referência, verifique se a usuário Sarah Rose está adicionada. As credenciais de login da Sarah são `srose/password`.

## John Jacobs recebe e aprova o aplicativo {#john-jacobs-receives-and-approves-the-application}

John Jacobs recebe as solicitações e as encaminha à pessoa certa. AEM Caixa de entrada permite que ela veja todos os aplicativos enviados em um único local.

### Como funciona {#how-it-works-1}

Quando Sarah preenche e envia o aplicativo FOIA, um registro do aplicativo é enviado para a caixa de entrada de John Jacobs. John Jacobs pode exibir o aplicativo enviado e aceitá-lo ou rejeitá-lo.

### Veja você mesmo {#see-it-yourself-1}

Você pode acessar a caixa de entrada AEM em https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Faça logon na caixa de entrada do AEM, usando jjacobs/password como nome de usuário/senha de John Jacobs, e consulte o aplicativo FOIA. Para obter informações sobre como usar AEM Caixa de entrada para tarefas de fluxo de trabalho centradas em formulários, consulte [Gerenciar aplicativos e tarefas do Forms na Caixa de entrada AEM](/help/forms/using/manage-applications-inbox.md).

![johnjacobs](assets/johnjacobs.png)

John Jacobs pode ver, aprovar ou rejeitar o aplicativo do painel do aplicativo. John Jacobs seleciona e abre os detalhes da solicitação e, depois de revisá-la, a aprova.

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah recebe um e-mail de confirmação</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

Depois que John Jacobs aprova o aplicativo, Sarah recebe um e-mail de confirmação do site We.Gov. Sarah é informada sobre as tarifas e o tempo necessário para processar seu pedido. O e-mail também inclui e-mail e detalhes do telefone. A sarah pode entrar em contato para obter atualizações sobre seu aplicativo.

![sarahroseemail](assets/sarahroseemail.png)

## Gloria recebe a solicitação FOIA para aprovação de segundo nível {#gloria-receives-the-foia-request-for-second-level-approval}

Depois que John Jacobs preenche as informações necessárias e aprova o pedido de Sarah, as solicitações vão para Gloria Rios para a aprovação final. Gloria revisa o documento de registro anexado e aprova a solicitação.

![gloriariosinbox](assets/gloriariosinbox.png)

### Como funciona {#how-it-works-2}

Quando John Jacobs aprova a solicitação FOIA, um PDF ou Documento de Registro da aplicação é criado e enviado para a caixa de entrada de Gloria Rios. Gloria pode exibir a solicitação enviada e aprová-la ou rejeitá-la.

### Veja você mesmo {#see-for-yourself}

Você pode acessar a caixa de entrada AEM em https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Faça logon na caixa de entrada do AEM usando grios/password como nome de usuário/senha para Gloria Rios e veja a solicitação FOIS.

Gloria abre o pedido e examina os detalhes do pedido FOIA. Depois de rever os detalhes do pedido e verificar a viabilidade de fornecer os documentos necessários, Gloria aprova o pedido.

![gloriariosaprovações](assets/gloriariosapproves.png)

## Sarah recebe notificação de que sua solicitação foi aprovada {#sarah-receives-notification-that-her-request-is-approved}

Depois que Gloria aprova a solicitação FOIA, Sarah recebe um e-mail notificando que sua solicitação foi aprovada. O e-mail também inclui informações sobre o cronograma indicativo para fornecer o documento e os detalhes de contato para acompanhamento do pedido.

![sarahroseemailapproval](assets/sarahroseemailapproval.png)
