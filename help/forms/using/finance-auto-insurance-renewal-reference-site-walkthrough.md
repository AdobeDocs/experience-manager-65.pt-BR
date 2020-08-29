---
title: Apresentação do site de referência de Renovação de Seguro Automático do We.Finance
seo-title: Apresentação do site de referência de Renovação de Seguro Automático do We.Finance
description: 'null'
seo-description: 'null'
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---


# Apresentação do site de referência de Renovação de Seguro Automático do We.Finance{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## Cenário do Site de Referência do We.Finance  {#we-finance-reference-site-scenario}

We.Finance site é um site de serviços financeiros projetado para ajudá-lo a conhecer os recursos interativos de comunicação da AEM Forms.

Leia a apresentação detalhada do caso de uso do We.Finance Auto Insurance que mostra como os formulários AEM e sua integração com o Microsoft Dynamics ajudam a personalizar a experiência do cliente em uma empresa de serviço financeiro. A apresentação interativa foi projetada para facilitar a implementação de transações digitais complexas e a comunicação do cliente em uma empresa financeira.

**A viagem start com o caso de utilização:**

Sarah Rose é uma cliente existente da We.Finance e comprou uma apólice de seguro de automóveis. Agora é a hora do ano para renovar sua apólice de seguro. Gloria Rios, Agente de Seguros, We.Finance envia um lembrete para Sarah sobre sua renovação de apólice. Sarah segue as instruções fornecidas no email e conclui com êxito o processo.

## Apresentação da aplicação de seguro automático {#auto-insurance-application-walkthrough}

O cenário do aplicativo We.Finance AutoInsurance é uma narração visual para o usuário e é baseado em duas pessoas:

* Sarah Rose, uma cliente We.Finance
* Gloria Rios, Agente de Seguros, We.Finance

### Gloria envia uma comunicação de renovação da apólice de seguro do We.Finance {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria entra em AEM instância, clica em Renovação **automática de seguro e,** em seguida, clica em **Abrir interface do usuário do agente.** O clique pré-preenche o documento com detalhes da apólice da Sarah Rose. Gloria clica **em Enviar** e uma mensagem é exibida na tela &quot;Enviar iniciado&quot; e em alguns segundos &quot;Enviado com êxito&quot;.

Sarah recebe um email com o assunto &quot;Sua renovação do seguro automático&quot;.

![IU do agente](assets/agent_ui_email_new.png)

#### Veja você mesmo {#see-it-yourself}

Vá para **Adobe Experience Manager** > **Forms** > **Forms e Documentos** > **We.Finance** > **Auto Insurance**. Selecione a comunicação **** interativa Renovação automática de seguro e clique em **Abrir interface do usuário** do agente. A comunicação interativa é aberta na interface do usuário do agente. Insira um endereço de email válido para receber o email com o documento de política anexado e clique em Enviar.

Você pode acessar e revisar a comunicação interativa Renovação automática de seguro diretamente de `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### Sarah recebe uma comunicação de renovação da apólice de seguro da We.Finance e decide renovar {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah recebe um email com um anexo do We.Finance que a lembra que sua apólice de Seguro Automático está prestes a expirar. O anexo é a versão impressa da carta de Seguro Automático.

Sarah clica em **Renove Now (Renovar agora** ) e é direcionada para a versão da Web de sua carta de Seguro Automático. Além desta carta, Sarah encontra o número de dias que faltam para sua política expirar. A página fornece a Sarah uma visão geral básica dos detalhes da Política de Seguro, como Número da Política, Quantia Devida e outras informações, como ofertas de desconto e recompensas por fidelidade. Sarah clica novamente em **Renovar agora** na parte inferior da política.

![ref1](assets/ref1.png)

#### Como funciona {#how-it-works}

A saída da Web e da impressão da carta de Seguro Automático são criadas usando os recursos de vários canais das Comunicações Interativas.

O botão Renovar agora no email está vinculado ao aplicativo Renovação de seguro automático, que é uma comunicação interativa em uma instância de publicação.

#### Veja você mesmo {#see-it-yourself-1}

Você deve ter recebido um email com um PDF anexado. O PDF é uma versão impressa da carta de Seguro Automático. Clique em **Renovar agora** para acessar a versão da Web da política. Verifique suas informações pessoais e detalhes de políticas e clique em **Renovar agora** , o que leva você para outra Comunicação interativa.

O botão **Renovar agora** no email direciona Sarah para a versão da Web da política. Você pode visitar o seguinte URL:

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

Você pode verificar o resumo detalhado da Renovação de seguro automático e clicar em **Renovar agora** na parte inferior da página.

### Sarah chega à página de pagamento {#sarah-reaches-the-payment-page}

We.Finance leva Sarah para a página Pagamento. Sarah reverifica o número da política e a data de expiração com seus registros. No lado direito da página, ela verifica o Resumo do Pagamento de sua renovação com 10% de desconto no valor total.

#### Como funciona {#how-it-works-1}

O botão Renovar agora direciona a Sarah para a página de pagamento. A página de pagamento é um formulário adaptável.

#### Veja você mesmo {#see-it-yourself-2}

Clique em **Renovar agora** para acessar a página Pagamento. Preencha as informações do Cartão de crédito e clique em **Efetuar pagamento**.

Você pode acessar a página de pagamento na instância de criação em

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah faz o pagamento e completa o processo {#sarah-makes-the-payment-and-completes-the-process}

Sarah preenche os detalhes do Cartão de Crédito e clica em **Fazer Pagamento**.

#### Como funciona {#how-it-works-2}

Quando Sarah preenche os detalhes do cartão de crédito e clica em Enviar, o pagamento do cartão de crédito é processado e uma mensagem de agradecimento configurada no formulário adaptável é exibida na tela.

#### Veja você mesmo {#see-it-yourself-3}

Você pode visualização a mensagem de confirmação depois de clicar em Efetuar pagamento em

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
