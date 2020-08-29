---
title: Apresentação do sítio de referência relativo a We.Gov FOIA
seo-title: Apresentação do sítio de referência relativo a We.Gov FOIA
description: Consulte o site de referência We.Gov para entender como a AEM Forms ajuda os governos a receber e entregar informações solicitadas por indivíduos sob a Lei de Liberdade de Informação.
seo-description: Consulte o site de referência We.Gov para entender como a AEM Forms ajuda os governos a receber e entregar informações solicitadas por indivíduos sob a Lei de Liberdade de Informação.
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---


# Apresentação do sítio de referência relativo a We.Gov FOIA {#we-gov-reference-site-foia-walkthrough}

## Cenário do Ato de Liberdade de Informação do Site de Referência {#reference-site-freedom-of-information-act-scenario}

We.Gov é uma organização estatal que permite que pais adotivos se inscrevam para o suporte infantil se eles adotarem uma criança. We.Gov também permite que os pais solicitem informações aos seguintes departamentos governamentais sob a lei de liberdade de informação:

* Agência de Logística da Defesa
* Departamento de Defesa do Serviço de Inspetores-Geral
* Departamento de Justiça - Gabinete de Política de Informação
* Departamento da Marinha
* Agência de Proteção Ambiental

Para obter mais informações sobre a Lei de Liberdade de Informação, consulte [www.foia.gov](https://www.foia.gov).

O cenário envolve as seguintes personas:

* Sarah Rose, a pessoa que solicita informações sob
* John Jacobs, o responsável pelo pedido, encaminha-o para o departamento adequado
* Gloria Rios, funcionária do governo que fornece as informações conforme o pedido

## Sarah dá início a um pedido de informações ao abrigo da FOIA {#sarah-initiates-request-for-information-under-foia}

Sob a Lei de Liberdade de Informação, Sarah solicita uma cópia dos registros de processos da Administração para Crianças e Famílias por anos (FY) 2013 até 2016. Sarah submete este pedido ao Departamento de Justiça - Gabinete de Política de Informação e significa também que está disposta a pagar até 100 dólares para os custos de impressão e envio de correio.

### Como funciona {#how-it-works}

### Veja você mesmo {#see-it-yourself}

No seu navegador, abra `https://<hostname>:<PublishPort>/wegov`. No site We.Gov, toque em Aplicativos > Todos os aplicativos. Na página Todos os aplicativos, toque em Aplicar sob Solicitação FOIA.

## Sarah start seu pedido de informações dentro da FOIA {#sarah-starts-her-application-for-information-under-foia}

Sarah clica em **Aplicar** e, na página Formulário de solicitação do Ato de Liberdade de Informação, digita as seguintes informações:

* **Agência:** Sarah especifica a agência para a qual o pedido foi dirigido como Departamento de Justiça - Escritório de Política de Informação.

* **Pagará Até**: Sarah especifica que está disposta a pagar até 100 dólares para as despesas de impressão e envio de correio.
* **Descreva a solicitação em detalhes**: Sarah especifica &quot;Solicitando cópia dos registros de caso da Administração para Crianças e Famílias para os anos fiscais de 2013 a 2016.&quot;

![Solicitação de cópia dos registros de caso da Administração para Crianças e Famílias para os exercícios fiscais de 2013 a 2016](assets/sarahfiosform.png)

Solicitação de cópia dos registros de caso da Administração para Crianças e Famílias para os exercícios fiscais de 2013 a 2016

A qualquer momento, Sarah pode tocar em Salvar para salvar o rascunho do formulário e retornar mais tarde para preencher o formulário e enviá-lo. Sarah submete o formulário.

>[!NOTE]
>
>O fluxo de trabalho de retornar do e-mail funciona somente com usuários conectados. No cenário do site de referência, verifique se a usuário Sarah Rose está adicionada. As credenciais de login da Sarah são `srose/password`.

## John Jacobs recebe e aprova a candidatura {#john-jacobs-receives-and-approves-the-application}

John Jacobs recebe os pedidos e os encaminha para a pessoa certa. AEM Caixa de entrada permite que ela veja todas as solicitações enviadas em um único lugar.

### Como funciona {#how-it-works-1}

Quando Sarah preenche e envia o pedido FOIA, um registro do pedido é enviado para a caixa de entrada de John Jacobs. John Jacobs pode visualização o pedido e aceitá-lo ou rejeitá-lo.

### Veja você mesmo {#see-it-yourself-1}

Você pode acessar a caixa de entrada AEM em https://&lt;nome do ***host***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Faça logon na caixa de entrada AEM usando jjacobs/password como o nome de usuário/senha de John Jacobs e consulte o aplicativo FOIA. Para obter informações sobre como usar AEM Caixa de entrada para tarefas de fluxo de trabalho centradas em formulários, consulte [Gerenciar aplicativos e tarefas do Forms AEM Caixa de entrada](/help/forms/using/manage-applications-inbox.md).

![johnjacobs](assets/johnjacobs.png)

John Jacobs pode ver, aprovar ou rejeitar o aplicativo do painel do aplicativo. John Jacobs seleciona e abre os detalhes da solicitação e, depois de revisá-la, a aprova.

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah recebe um email de reconhecimento</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

Depois que John Jacobs aprovar o aplicativo, Sarah recebe um e-mail de reconhecimento do site We.Gov. Sarah é informada sobre as taxas e o tempo necessários para processar seu pedido. O e-mail também inclui e-mail e detalhes telefônicos que a Sarah pode contactar para obter atualizações sobre o seu aplicativo.

![sarahroseemail](assets/sarahroseemail.png)

## Gloria recebe o pedido FOIA de aprovação de segundo nível {#gloria-receives-the-foia-request-for-second-level-approval}

Depois que John Jacobs preenche as informações exigidas e aprova o pedido de Sarah, os pedidos vão para Gloria Rios para a aprovação final. Gloria revisa o documento de registro anexado e aprova o pedido.

![gloriariosinbox](assets/gloriariosinbox.png)

### Como funciona {#how-it-works-2}

Quando John Jacobs aprova a solicitação FOIA, um PDF ou Documento de Record é criado e enviado para a caixa de entrada de Gloria Rios. Gloria pode visualização o pedido enviado e aprová-lo ou rejeitá-lo.

### Veja você mesmo {#see-for-yourself}

Você pode acessar a caixa de entrada AEM em https://&lt;nome do ***host***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Faça logon na caixa de entrada AEM usando grios/password como nome de usuário/senha para Gloria Rios e consulte a solicitação FOIS.

Gloria abre o pedido e examina os detalhes do pedido FOIA. Depois de rever os detalhes do pedido e verificar a viabilidade de fornecer os documentos requeridos, Gloria aprova o pedido.

![gloriariosaprovações](assets/gloriariosapproves.png)

## Sarah recebe uma notificação de que seu pedido foi aprovado {#sarah-receives-notification-that-her-request-is-approved}

Depois que Gloria aprova a solicitação FOIA, Sarah recebe um e-mail notificando-a de que sua solicitação foi aprovada. O e-mail também inclui as informações sobre o cronograma provisório para fornecer o documento e os detalhes de contato para o acompanhamento da solicitação.

![sarahroseemailApproval](assets/sarahroseemailapproval.png)

