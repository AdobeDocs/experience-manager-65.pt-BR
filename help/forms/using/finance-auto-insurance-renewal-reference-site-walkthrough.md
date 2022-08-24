---
title: Apresentação do site de referência da renovação do seguro automático We.Finance
seo-title: We.Finance Auto Insurance Renewal reference site walkthrough
description: Apresentação do site de referência da renovação do seguro automático We.Finance
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
exl-id: b6ded6ac-4fb1-49f9-b272-16774c3e89a3
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# Apresentação do site de referência da renovação do seguro automático We.Finance{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## Cenário do site de referência We.Finance  {#we-finance-reference-site-scenario}

We.Finance é um site de serviços financeiros criado para ajudá-lo a aprender os recursos interativos de comunicação do AEM Forms.

Leia a apresentação detalhada do caso de uso do We.Finance Auto Insurance, que mostra como os formulários de AEM e sua integração com o Microsoft Dynamics ajudam a personalizar a experiência do cliente em uma empresa de serviços financeiros. A apresentação interativa foi criada para facilitar a implementação de transações digitais complexas e a comunicação com o cliente em uma empresa financeira.

**A jornada começa com o caso de uso:**

Sarah Rose é uma cliente We.Finance existente e comprou uma apólice de seguro de automóvel. Agora é a hora do ano para a renovação de sua apólice de seguro. Gloria Rios, Agente de Seguro, We.Finance envia um lembrete para Sarah sobre a renovação de sua apólice. Sarah segue as instruções fornecidas no email e conclui com sucesso o processo.

## Apresentação do pedido de seguro automático {#auto-insurance-application-walkthrough}

O cenário de aplicação We.Finance Auto Insurance é uma narração visual para o usuário e é baseado em duas personas:

* Sarah Rose, uma cliente We.Finance
* Gloria Rios, Agente de Seguro, We.Finance

### Gloria envia uma comunicação de renovação da apólice de seguro do We.Finance {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria entra AEM instância, clica em **Renovação de Seguro Automático,** e, em seguida, cliques **Abra a interface do usuário do agente.** O clique preenche o documento de seguro com detalhes da apólice de Sarah Rose. Gloria clica **Enviar** e uma mensagem é exibida na tela &quot;Envio iniciado&quot; e em alguns segundos &quot;Enviado com êxito&quot;.

Sarah recebe um email com o assunto &quot;Sua renovação do seguro automático&quot;.

![IU do agente](assets/agent_ui_email_new.png)

#### Veja você mesmo {#see-it-yourself}

Ir para **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents** > **We.Finance** > **Seguro Automático**. Selecione a Renovação de Seguro Automático **comunicação interativa** e clique em **Abrir interface do usuário do agente**. A comunicação interativa é aberta na interface do usuário do agente. Digite um endereço de email válido para receber o email com o documento de política anexado e clique em Enviar.

Você pode acessar e revisar a comunicação interativa Renovação de seguro automático diretamente de `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### Sarah recebe uma comunicação de renovação de apólice de seguro do We.Finance e decide renovar {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah recebe um e-mail com um anexo do We.Finance que lembra que sua apólice de Seguro Automático está prestes a expirar. O anexo é a versão impressa da carta de Seguro Automático.

Sarah clica **Renovar agora** e é direcionado para a versão da Web da carta de Seguro Automático. Além desta carta, Sarah encontra o número de dias que faltam para que sua política expire. A página fornece a Sarah uma visão geral básica dos detalhes da Política de seguro, como Número da Política, Quantia Devida e outras informações, como ofertas de desconto e recompensas por fidelidade. Sarah novamente clica **Renovar agora** na base da política.

![ref1](assets/ref1.png)

#### Como funciona {#how-it-works}

A saída da Web e impressão da carta de Seguro Automático é criada usando os recursos de vários canais das Comunicações interativas.

O botão Renovar agora no email é vinculado ao aplicativo Renovação de seguro automático, que é uma comunicação interativa em uma instância de publicação.

#### Veja você mesmo {#see-it-yourself-1}

Você deve ter recebido um email com um PDF anexado. O PDF é uma versão impressa da carta de Seguro Automático. Clique em **Renovar agora** para acessar a versão da web da política. Verifique suas informações pessoais e detalhes de política e clique em **Renovar agora** que leva você a outra Comunicação interativa.

O **Renovar agora** no email direciona a Sarah para a versão da web da política. Você pode visitar o seguinte URL:

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

Você pode verificar o resumo detalhado da renovação do seguro automático e clicar em **Renovar agora** na parte inferior da página.

### Sarah chega à página de pagamento {#sarah-reaches-the-payment-page}

We.Finance leva Sarah à página de pagamento. Sarah reverifica o número da política e a data de expiração com seus registros. No lado direito da página, ela verifica o Resumo do Pagamento de sua renovação com 10% de desconto no valor total.

#### Como funciona {#how-it-works-1}

O botão Renovar agora direciona a Sarah para a página de pagamento. A página de pagamento é um formulário adaptável.

#### Veja você mesmo {#see-it-yourself-2}

Clique em **Renovar agora** para acessar a página Pagamento. Preencha as informações do Cartão de crédito e clique em **Fazer pagamento**.

Você pode acessar a página de pagamento na instância de criação em

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah faz o pagamento e conclui o processo {#sarah-makes-the-payment-and-completes-the-process}

Sarah preenche os detalhes e os cliques do cartão de crédito **Fazer pagamento**.

#### Como funciona {#how-it-works-2}

Quando Sarah preenche os detalhes do cartão de crédito e clica em Enviar, o pagamento do cartão de crédito é processado e uma mensagem de agradecimento configurada no formulário adaptável aparece na tela.

#### Veja você mesmo {#see-it-yourself-3}

Você pode exibir a mensagem de confirmação depois de clicar em Fazer pagamento em

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
