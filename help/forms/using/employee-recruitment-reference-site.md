---
title: Apresentação do site de referência de recrutamento do funcionário
description: O site de referência do AEM Forms mostra como as organizações podem usar os recursos do AEM Forms para implementar o workflow de recrutamento de funcionários.
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: bdfc0a20-1e98-47f9-a1d1-5af5b3ef15db
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Foundation Components
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1417'
ht-degree: 0%

---

# Apresentação do site de referência de recrutamento do funcionário {#employee-recruitment-reference-site-walkthrough}

## Visão geral {#overview}

We.Finance é uma organização que permite que os candidatos se candidatem a emprego por meio do portal do site de referência. A organização também usa o portal para gerenciar o agendamento de entrevistas, a pré-seleção e a comunicação interna dos candidatos. O site gerencia o seguinte:

* Candidatos que procuram e se candidatam a cargos
* Seleção e pré-seleção dos candidatos
* Processo de entrevista
* Coleta de detalhes do candidato
* Verificação dos antecedentes dos candidatos
* Distribuindo ofertas aos candidatos selecionados

>[!NOTE]
>
>Os casos de uso de recrutamento de funcionários estão disponíveis nos sites de referência We.Finance e We.Gov. Os exemplos, as imagens e as descrições usadas nas apresentações usam o site de referência We.Finance. No entanto, você pode executar esses casos de uso e revisar artefatos usando o We.Gov também. Para fazer isso, substitua **we-finance** com **we-gov** nos URLs mencionados.

### Modelos de fluxo de trabalho envolvidos {#workflow-models-involved}

O caso de uso de recrutamento de funcionários envolve dois workflows:

* Antes da entrevista - Financiamos o fluxo de trabalho de recrutamento de funcionários
* Após a entrevista - Financiamos o workflow Pós-Entrevista de Recrutamento de Funcionário

Esses workflows são criados no AEM e podem ser encontrados em:

`https://[authorHost]:[authorPort]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models/`

#### Financiamos o fluxo de trabalho de recrutamento de funcionários {#we-finance-employee-recruiting-workflow}

A seguir está o modelo do fluxo de trabalho Recrutamento de Funcionário das Finanças seguido neste documento.

![we-finance-employee-recruiting-workflow](assets/we-finance-employee-recruiting-workflow.png)

#### Fluxo de trabalho de pós-entrevista do recrutamento de funcionários do We Finance {#we-finance-employee-recruiting-post-interview-workflow}

A seguir está o modelo do fluxo de trabalho Recrutamento Pós-Entrevista de Funcionário das Finanças seguido neste documento.

![we-finance-employee-recrutiting-post-entrevista-workflow](assets/we-finance-employee-recruiting-post-interview-workflow.png)

### Personas {#personas}

O cenário envolve os seguintes perfis:

* Sarah Rose, a candidata que se candidata a um emprego na organização
* John Jacobs, o recrutador
* Gloria Rios, a gerente de contratação
* John Doe, o RH

## Sarah se candidata a um emprego {#sarah-applies-for-a-job}

Sarah Rose está procurando uma oportunidade de trabalho na organização. Ela visita o portal da web e explora as vagas de emprego listadas na página Carreira. Ela encontra uma lista de empregos correspondente e se candidata a ela.

![home-page](assets/home-page.png)

Página inicial do We.Finance

![página-carreira](assets/career-page.png)

Página de carreira do We.Finance

Sarah clica em Aplicar em uma publicação de trabalho. O formulário de solicitação de emprego é aberto. Ela preenche todos os detalhes do pedido e o envia.

![job-application-form](assets/job-application-form.png)

### Como funciona {#how-it-works}

A página inicial do We.Finance e a página de carreira são páginas do AEM Sites. A página de carreira incorpora um formulário adaptável, que usa um painel repetível para buscar vagas de trabalho usando um serviço e listá-las na página. Você pode revisar o formulário adaptável em `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/recruitment/jobs.html`.

### Veja você mesmo {#see-it-yourself}

Ir para `https://[publishHost]:[publishPort]/content/we-finance/global/en.html` e clique em **[!UICONTROL Carreira]**. Clique em **[!UICONTROL Pesquisar]** para preencher a lista de trabalhos e, em seguida, clique em **[!UICONTROL Aplicar]** para um trabalho. Preencha os detalhes no formulário e envie a solicitação.

Certifique-se de especificar uma ID de e-mail válida no aplicativo, pois qualquer comunicação por meio dessa apresentação será enviada para a ID de e-mail especificada.

## Perfil de Sarah Rose na lista de candidatos de John Jacobs para a triagem do gerente de contratação {#john-jacobs-shortlists-sarah-rose-s-profile-for-the-hiring-manager-s-screening}

A organização recebe a requisição de cargo submetida por Sarah. John Jacobs, um recrutador, é designado para revisar o perfil de Sarah. John analisa a tarefa em sua Caixa de entrada AEM, encontra o perfil que corresponde ao requisito da tarefa e clica em Shortlist. O perfil de Sarah é encaminhado para Gloria Rios, a gerente de contratação, para sua aprovação.

![jjacobs-inbox-1](assets/jjacobs-inbox-1.png)

Caixa de entrada AEM de John

![candidate-shortlist](assets/candidate-shortlist.png)

Perfil de Sarah Rose na lista de candidatos de John Jacobs para a triagem do gerente de contratação

**Como funciona**

A ação de submissão no form Requisição de Cargo aciona um workflow que cria uma tarefa na caixa de entrada de John Jacob para filtrar a requisição. Quando John, revisa e pré-seleciona o aplicativo, o workflow cria uma tarefa na caixa de entrada do gerente de contratação, Gloria.

### Veja você mesmo {#see-it-yourself-1}

Ir para `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`e faça logon usando jacobs/password como nome de usuário/senha de John Jacobs. Abra a tarefa Revisão de Perfil do Candidato e selecione o candidato.

## Gloria analisa o pedido e aprova o candidato para uma entrevista {#gloria-reviews-the-application-and-approves-the-applicant-for-an-interview}

Gloria, a gerente de contratação, recebe o perfil selecionado como uma tarefa em sua Caixa de entrada AEM. Ela revisa e aprova a candidata, Sarah Rose, para a entrevista.

![gloriainbox](assets/gloriainbox.png)

Caixa de entrada do AEM de Gloria

![gloriaschedulesentrevista](assets/gloriaschedulesinterview.png)

Gloria aprova Sarah Rose para uma entrevista

**Como funciona**

Quando Gloria aprova o candidato para uma entrevista, o workflow cria uma tarefa na Caixa de entrada AEM de John Doe, que é recrutador da We.Finance.

### Veja você mesmo {#see-it-yourself-2}

Ir para `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` e faça logon usando jacobs/password como nome de usuário/senha de John Jacobs. Abra a tarefa Revisão de Perfil do Candidato e selecione o candidato.

Ir para `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` e faça login usando grios/password como nome de usuário/senha de Gloria Rios. Abra a tarefa Revisão de Perfil do Candidato e clique em Agendar Entrevista.

## John Doe agenda uma entrevista {#john-doe-schedules-an-interview}

John Doe recebe a tarefa de agendar uma entrevista em sua caixa de entrada. John Doe seleciona e abre a tarefa e fixa a data e hora da entrevista, o local e a pessoa de RH responsável pela entrevista como John Jacob. John Doe clica em Enviar e-mail de convite. Um email é enviado para Sarah e uma tarefa é atribuída a Gloria, a gerente de contratação, para entrevistar Sarah.

![johnjacobsaeminbox](assets/johnjacobsaeminbox.png)

Caixa de entrada AEM de John Doe

![johndoescheduleentrevista](assets/johndoescheduleinterview.png)

John Doe agenda a entrevista e envia os detalhes para Sarah Rose

## Sarah Rose recebe o e-mail com a programação da entrevista {#sarah-rose-receives-the-email-with-interview-schedule}

Sarah Rose recebe o email com cronograma de entrevistas, local e outros detalhes. Sarah clica em Accept para indicar que está bem com o cronograma e o local da entrevista. Como guiado pela informação precisa, Sarah chega às entrevistas.

![sarahroseinterviewemail](assets/sarahroseinterviewemail.png)

Sarah Rose recebe o cronograma da entrevista

## Após as entrevistas, a gerente de contratação lista Sarah Rose {#after-the-interviews-the-hiring-manager-shortlists-sarah-rose}

Depois que Sarah Rose passa pelas entrevistas e as limpa, Gloria Rios, a gerente de contratação, abre a tarefa Seleção de Candidatos em sua caixa de entrada e clica em Selecionar. A decisão de Gloria Rios é transmitida para a pessoa do RH, John Doe, para processamento adicional.

![gloriariosinboxoffer](assets/gloriariosinboxoffer.png)

Caixa de entrada do AEM de Gloria

![gloriariosselectcandidate](assets/gloriariosselectcandidate.png)

Gloria Rios seleciona Sarah Rose após as entrevistas

## John Doe solicita mais informações {#john-doe-requests-more-information}

Antes de pedir a um candidato para se juntar à organização, os antecedentes de Sarah devem ser verificados. John Doe abre e revisa os detalhes da candidata selecionada e descobre que alguns de seus detalhes de emprego e educação ainda não foram preenchidos. Cliques do John Doe Precisam de mais informações.

![johndoeinbox](assets/johndoeinbox.png) ![johndoeneedmoreinformation](assets/johndoeneedmoreinformation.png)

John Doe pede mais informações de Sarah Rose sobre sua educação e experiência de trabalho

## Sarah Rose recebe um email solicitando mais informações {#sarah-rose-receives-an-email-requesting-further-information}

Sarah Rose recebe um e-mail notificando-a de que mais informações são necessárias para processar sua solicitação de emprego. O email inclui um link para o formulário para preencher as informações necessárias.

![sarahroseemailmoredetails](assets/sarahroseemailmoredetails.png)

Sarah Rose recebe um e-mail notificando que informações adicionais são necessárias para processar sua solicitação de emprego

Sarah clica no link Fornecer detalhes no email. Um formulário é exibido. Sarah preenche os detalhes necessários de educação e emprego, conforme solicitado por John Doe e clica em Enviar.

![informaçõesadicionais1](assets/additionalinformation1.png)

Sarah abre o formulário de informações adicionais clicando no link no email

![informaçõesadicionais2](assets/additionalinformation2.png)

Sarah preenche as informações adicionais solicitadas por John Doe e clica em Enviar

## John Doe analisa o perfil de candidato selecionado para obter as informações adicionais fornecidas {#john-doe-reviews-the-selected-candidate-profile-for-the-additional-information-provided}

John Doe seleciona a solicitação de revisão do candidato e a abre. John Doe descobre que Sarah preencheu todas as informações necessárias. Depois de revisar o aplicativo, John Doe clica em Aprovar. Após a aprovação por John Doe, o pedido para realizar uma verificação de antecedentes em Sarah Rose é encaminhado a John Jacobs.

![johndoeadditionainformationinbox](assets/johndoeadditionainformationinbox.png)

Caixa de entrada AEM de John Doe

![johndoeadditionalinformationreview-copy](assets/johndoeadditionalinformationreview-copy.png)

John Doe analisa as informações adicionais fornecidas por Sarah e as aprova

## John Jacobs recebe uma solicitação de verificação de experiência {#john-jacobs-receives-a-background-check-request}

John Jacobs vê a solicitação de verificação de histórico em sua caixa de entrada. John Jacobs abre a tarefa e analisa as informações fornecidas por Sarah Rose. Depois de executar uma verificação de histórico, John Jacobs clica em Ir em frente para indicar que a verificação de histórico foi bem-sucedida.

![johnjacobsbackgroundcheckinbox](assets/johnjacobsbackgroundcheckinbox.png)

Caixa de entrada AEM de John Jacobs

![johnjacobsbackgroundcheckgoahead](assets/johnjacobsbackgroundcheckgoahead.png)

Depois de executar a verificação de background, John Jacobs clica em Ir adiante

## John Doe envia a carta de adesão para Sarah Rose {#john-doe-sends-out-the-joining-letter-to-sarah-rose}

John Doe recebe uma solicitação em sua Caixa de entrada do AEM para enviar a carta de associação. John abre a solicitação e visualiza os detalhes. John Doe anexa a PDF da carta de junção e clica em Anexar e enviar carta de junção.

![johndoejoiningletterinbox](assets/johndoejoiningletterinbox.png)

Caixa de entrada AEM de John Doe

![johndoejoiningletterattachandsend](assets/johndoejoiningletterattachandsend.png)

João Silva envia a carta de adesão para assinatura

## Sarah Rose recebe e assina a carta de adesão {#sarah-rose-receives-and-signs-the-joining-letter}

Sarah Rose recebe a carta de adesão por assinar. Sarah Clica Clique Aqui Para Revisar E Assinar A Carta De Junção. A PDF da carta de junção é aberta com um campo para assinar o documento.

![sarahrosejoiningletteremail](assets/sarahrosejoiningletteremail.png)

Sarah Rose recebe a carta de adesão por assinar

Sarah pode optar por digitar, usar desenhar para escrever à mão, inserir uma imagem de assinatura ou usar a tela de toque de seu celular para desenhar sua assinatura. Sarah digita seu nome, clica em Clique para assinar e baixa a cópia assinada da carta de associação.

![sarahrosejoininglettersign](assets/sarahrosejoininglettersign.png)

Sarah digita seu nome para assinar a carta de associação

![sarahrosejoininglettersign2](assets/sarahrosejoininglettersign2.png)

Sarah clica em Clique para assinar para concluir a assinatura da carta de associação
