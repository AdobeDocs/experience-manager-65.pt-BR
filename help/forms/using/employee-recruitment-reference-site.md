---
title: Apresentação do site de referência de recrutamento de funcionários
seo-title: Employee recruitment
description: O site de referência do AEM Forms mostra como as organizações podem usar os recursos do AEM Forms para implementar o fluxo de trabalho de recrutamento de funcionários.
seo-description: AEM Forms reference site showcases how organizations can use AEM Forms features to implement employee recruitment workflow.
uuid: 27e456ba-3c08-4c43-ad54-1ba0070995ad
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f04b13e-ea40-4c86-9168-e020c52435a2
exl-id: bdfc0a20-1e98-47f9-a1d1-5af5b3ef15db
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 0%

---

# Apresentação do site de referência de recrutamento de funcionários {#employee-recruitment-reference-site-walkthrough}

## Visão geral {#overview}

We.Finance é uma organização que permite aos candidatos candidatarem-se ao emprego através do portal do site de referência. A organização também usa o portal para gerenciar o agendamento de entrevistas dos candidatos, a pré-listagem e a comunicação interna. O site gerencia o seguinte:

* Candidatos que procuram e se candidatam a empregos
* Rastreio e pré-seleção dos candidatos
* Processo de entrevista
* Recolha de dados relativos aos candidatos
* Verificação em segundo plano do candidato
* Implantação de ofertas para candidatos selecionados

>[!NOTE]
>
>Os casos de uso de recrutamento de funcionários estão disponíveis nos sites de referência We.Finance e We.Gov . Os exemplos, imagens e descrições usados nas orientações usam o site de referência We.Finance. No entanto, você também pode executar esses casos de uso e revisar artefatos usando We.Gov. Para fazer isso, substitua **cofinanciamento** com **we-gov** nos URLs mencionados.

### Modelos de workflow envolvidos {#workflow-models-involved}

O caso de uso de recrutamento de funcionários envolve dois workflows:

* Antes da entrevista - Fluxo de trabalho de recrutamento de funcionários do We Finance
* Após a entrevista - Workflow de Pós-Entrevista de Recrutamento de Funcionário do We Finance

Esses workflows são criados no AEM e podem ser encontrados em:

`https://[authorHost]:[authorPort]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models/`

#### Fluxo de trabalho Recrutamento de Funcionário do We Finance {#we-finance-employee-recruiting-workflow}

Este é o modelo do workflow de Recrutamento de Funcionário do We Finance seguido neste documento.

![we-finance-employee-recruting-workflow](assets/we-finance-employee-recruiting-workflow.png)

#### Workflow de Pós-Entrevista de Recrutamento de Funcionário do We Finance {#we-finance-employee-recruiting-post-interview-workflow}

Este é o modelo do workflow de Recrutamento de Post Entrevista do Funcionário do We Finance seguido neste documento.

![we-finance-employee-recruting-post-entrevista-workflow](assets/we-finance-employee-recruiting-post-interview-workflow.png)

### Personas {#personas}

O cenário envolve as seguintes personas:

* Sarah Rose, candidata a emprego na organização
* John Jacobs, o recrutador
* Gloria Rios, gerente de contratação
* John Doe, o homem do HR

## Sarah pede um emprego {#sarah-applies-for-a-job}

Sarah Rose está procurando emprego na organização. Ela visita seu portal na web e explora as vagas de emprego listadas na página Carreira. Ela encontra uma lista de empregos correspondente e se aplica a ela.

![página inicial](assets/home-page.png)

Página inicial do We.Finance

![página da carreira](assets/career-page.png)

Página de carreira We.Finance

Sarah clica em Aplicar em uma publicação de trabalho. O formulário de aplicativo de trabalho é aberto. Ela preenche todos os detalhes do pedido e o submete.

![job-application-form](assets/job-application-form.png)

### Como funciona {#how-it-works}

A página inicial do We.Finance e a página de carreira são páginas do AEM Sites. A página de carreira incorpora um formulário adaptável, que usa um painel repetível para buscar ofertas de emprego usando um serviço e listá-las na página. Você pode revisar o formulário adaptável em `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/recruitment/jobs.html`.

### Veja você mesmo {#see-it-yourself}

Ir para `https://[publishHost]:[publishPort]/content/we-finance/global/en.html` e clique em **[!UICONTROL Carreira]**. Clique em **[!UICONTROL Pesquisar]** para preencher a lista de tarefas e clique em **[!UICONTROL Aplicar]** para um emprego. Preencha os dados no formulário e envie o pedido.

Certifique-se de especificar uma ID de email válida no aplicativo, pois qualquer comunicação por meio dessa apresentação será enviada para a ID de email especificada.

## John Jacobs apresenta o perfil de Sarah Rose para a seleção do gerente de contratação {#john-jacobs-shortlists-sarah-rose-s-profile-for-the-hiring-manager-s-screening}

A organização recebe o pedido de emprego enviado pela Sarah. John Jacobs, recrutador, tem a tarefa de revisar o perfil de Sarah. Ele analisa a tarefa em sua Caixa de entrada de AEM, encontra o perfil correspondente ao requisito de trabalho e clica em Lista de atalhos. O perfil de Sarah é encaminhado a Gloria Rios, a gerente de contratação, para sua aprovação.

![jjacobs-inbox-1](assets/jjacobs-inbox-1.png)

Caixa de entrada de AEM do John

![candidato/lista restrita](assets/candidate-shortlist.png)

John Jacobs apresenta o perfil de Sarah Rose para a seleção do gerente de contratação

**Como funciona**

A ação de envio no formulário de Solicitação de trabalho aciona um fluxo de trabalho que cria uma tarefa na caixa de entrada de John Jacob para filtrar o aplicativo. Quando John, revisa e pré-insere o aplicativo, o workflow cria uma tarefa na caixa de entrada do gerente de contratação, Gloria.

### Veja você mesmo {#see-it-yourself-1}

Ir para `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`e faça logon usando jjacobs/password como nome de usuário/senha para John Jacobs. Abra a tarefa Revisão do perfil do candidato e coloque o candidato na lista de pré-requisitos.

## Gloria reexamina o pedido e aprova o recorrente para uma entrevista {#gloria-reviews-the-application-and-approves-the-applicant-for-an-interview}

Gloria, gerente de contratação, recebe o perfil pré-listado como uma tarefa em sua Caixa de entrada de AEM. Ela revisa e aprova a candidata, Sarah Rose, para a entrevista.

![gloriainbox](assets/gloriainbox.png)

Caixa de entrada AEM de Gloria

![gloriaschedulesentrevista](assets/gloriaschedulesinterview.png)

Gloria aprova Sarah Rose para entrevista

**Como funciona**

Quando Gloria aprova o candidato para uma entrevista, o fluxo de trabalho cria uma tarefa na Caixa de Entrada AEM de John Doe, que é um recrutador para We.Finance.

### Veja você mesmo {#see-it-yourself-2}

Ir para `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` e faça logon usando jjacobs/password como nome de usuário/senha para John Jacobs. Abra a tarefa Revisão do perfil do candidato e coloque o candidato na lista de pré-requisitos.

Ir para `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` e faça logon usando grios/password como nome de usuário/senha para Gloria Rios. Abra a tarefa Revisão do perfil do candidato e clique em Intervalo de programação.

## John Doe agenda uma entrevista {#john-doe-schedules-an-interview}

John Doe recebe a tarefa de agendar uma entrevista em sua caixa de entrada. John Doe seleciona e abre a tarefa e corrige a data e hora da entrevista, o local e a pessoa HR responsável pela entrevista como John Jacob. John Doe clica em Enviar Email de Convite. Um e-mail é enviado para Sarah e uma tarefa é atribuída a Gloria, a gerente de contratação, para entrevistar Sarah.

![johnjacobsaeminbox](assets/johnjacobsaeminbox.png)

Caixa de entrada de AEM de John Doe

![johndoescheduleentrevista](assets/johndoescheduleinterview.png)

John Doe agenda a entrevista e envia os detalhes para Sarah Rose

## Sarah Rose recebe o e-mail com a agenda da entrevista {#sarah-rose-receives-the-email-with-interview-schedule}

Sarah Rose recebe o e-mail com agendamento de entrevista, local e outros detalhes. Ela clica em Aceitar para indicar que está bem com o cronograma e o local da entrevista. Como guiada pela informação precisa, Sarah chega às entrevistas.

![sarahroseentreviewemail](assets/sarahroseinterviewemail.png)

Sarah Rose recebe o cronograma da entrevista

## Depois das entrevistas, a gerente de contratação ataca Sarah Rose {#after-the-interviews-the-hiring-manager-shortlists-sarah-rose}

Depois que Sarah Rose passar pelas entrevistas e limpar, Gloria Rios, a Gerente de Contratação, abre a tarefa Seleção de Candidatos a partir de sua caixa de entrada e clica em Selecionar. A decisão de Gloria Rios é transmitida ao HR, John Doe, para posterior processamento.

![gloriariosinboxoffer](assets/gloriariosinboxoffer.png)

Caixa de entrada AEM de Gloria

![gloriariosseletedCandidate](assets/gloriariosselectcandidate.png)

Gloria Rios seleciona Sarah Rose após as entrevistas

## John Doe solicita mais informações {#john-doe-requests-more-information}

Antes de solicitar que um candidato se junte à organização, é necessário verificar seu histórico. John Doe abre e revisa os detalhes da candidata selecionada e descobre que alguns de seus detalhes de emprego e educação ainda não estão preenchidos. Os cliques de John Doe precisam de mais informações.

![johndoeinbox](assets/johndoeinbox.png) ![johndoeneedmoreinformation](assets/johndoeneedmoreinformation.png)

John Doe solicita mais informações de Sarah Rose sobre sua educação e experiência de trabalho

## Sarah Rose recebe um email solicitando mais informações {#sarah-rose-receives-an-email-requesting-further-information}

Sarah Rose recebe um e-mail notificando-a de que são necessárias mais informações para processar seu pedido de emprego. O email inclui um link para o formulário para preencher as informações necessárias.

![sarahroseemailmoredetails](assets/sarahroseemailmoredetails.png)

Sarah Rose recebe um email notificando que informações adicionais são necessárias para processar seu pedido de emprego

Sarah clica no link Fornecer detalhes no email. Um formulário é exibido. Sarah preenche os detalhes de educação e emprego exigidos, conforme solicitado por John Doe e clica em Enviar.

![additionalinformation1](assets/additionalinformation1.png)

Sarah abre o formulário de informações adicionais clicando no link no email

![additionalinformation2](assets/additionalinformation2.png)

Sarah preenche as informações adicionais solicitadas por John Doe e clica em Enviar

## John Doe analisa o perfil do candidato selecionado para obter as informações adicionais fornecidas {#john-doe-reviews-the-selected-candidate-profile-for-the-additional-information-provided}

John Doe seleciona a solicitação de revisão do candidato e a abre. John Doe acha que Sarah encheu toda a informação conforme necessário. Após revisar o aplicativo, John Doe clica em Aprovar. Com a aprovação de John Doe, o pedido para fazer uma verificação de fundo de Sarah Rose é encaminhado a John Jacobs.

![johndoeadditional informationinbox](assets/johndoeadditionainformationinbox.png)

Caixa de entrada de AEM de John Doe

![johndoeadditional-informationreview-copy](assets/johndoeadditionalinformationreview-copy.png)

John Doe analisa as informações adicionais fornecidas por Sarah e aprova-as

## John Jacobs recebe uma solicitação de verificação em segundo plano {#john-jacobs-receives-a-background-check-request}

John Jacobs vê a solicitação de verificação de fundo em sua caixa de entrada. John Jacobs abre a tarefa e analisa as informações fornecidas por Sarah Rose. Após executar uma verificação em segundo plano, John Jacobs clica em Go Ahead para indicar que a verificação em segundo plano foi bem-sucedida.

![johnjacobsbackundercheckinbox](assets/johnjacobsbackgroundcheckinbox.png)

Caixa de entrada de AEM de John Jacobs

![johnjacobsbackunderundercheckahead](assets/johnjacobsbackgroundcheckgoahead.png)

Depois de executar a verificação de fundo, John Jacobs clica em Avançar

## John Doe envia a carta de adesão para Sarah Rose {#john-doe-sends-out-the-joining-letter-to-sarah-rose}

John Doe recebe uma solicitação em sua caixa de entrada de AEM para enviar a carta de junção. John abre a solicitação e exibe os detalhes. John Doe anexa a letra de junção PDF e, em seguida, clica em Anexar e enviar carta de junção.

![johndoejoiningletterinbox](assets/johndoejoiningletterinbox.png)

Caixa de entrada de AEM de John Doe

![johndoejoiningletterattachment](assets/johndoejoiningletterattachandsend.png)

John Doe envia a carta de junção para assinatura

## Sarah Rose recebe e assina a carta de ligação {#sarah-rose-receives-and-signs-the-joining-letter}

Sarah Rose recebe a carta de ligação por assinatura. Sarah clica Em Clique Aqui Para Revisar E Assinar Carta De Aderência. A PDF da letra de junção é aberta com um campo para assinar o documento.

![sarahrosejoiningletteremail](assets/sarahrosejoiningletteremail.png)

Sarah Rose recebe a carta de ligação por assinatura

Sarah pode optar por digitar, usar draw para escrever à mão, inserir uma imagem de assinatura ou usar a tela sensível ao toque de seu celular para desenhar sua assinatura. Sarah digita o nome, clica em Clicar para assinar e descarrega a cópia assinada da carta de junção.

![sarahrosejoininglettersign](assets/sarahrosejoininglettersign.png)

Sarah digita o nome para assinar a carta de adesão

![sarahrosejoininglettersign2](assets/sarahrosejoininglettersign2.png)

Sarah clica em Clicar para Assinar para concluir a assinatura da carta de associação
