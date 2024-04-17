---
title: Criação de uma página inicial efetiva de informativo
description: Uma página de aterrissagem eficaz do informativo ajuda você a obter o máximo de pessoas possível para se inscrever no seu informativo (ou outra campanha de marketing por email). Você pode usar as informações coletadas nas inscrições do seu boletim informativo para obter leads.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: c2fbf858-8815-426e-a2e5-f92bcf909ad0
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Criação de uma página inicial efetiva de informativo{#creating-an-effective-newsletter-landing-page}

Uma página de aterrissagem eficaz do informativo ajuda você a obter o máximo de pessoas possível para se inscrever no seu informativo (ou outra campanha de marketing por email). Você pode usar as informações coletadas nas inscrições do seu boletim informativo para obter leads.

Para criar uma landing page efetiva do boletim informativo, faça o seguinte:

1. Crie uma lista para o informativo para que as pessoas possam assiná-lo.
1. Crie o formulário de inscrição. Ao fazer isso, adicione uma etapa de fluxo de trabalho que adiciona automaticamente a pessoa que se inscreve no boletim informativo à sua lista de clientes potenciais.
1. Crie uma página de Confirmação que agradeça os usuários por se inscreverem e possivelmente forneça a eles uma promoção.
1. Adicione teasers.

>[!NOTE]
>
>A Adobe não pretende aprimorar ainda mais esse recurso (Gerenciamento de clientes em potencial e listas).
>A recomendação é usar [Adobe Campaign e a integração com o AEM](/help/sites-administering/campaign.md).

## Criação de uma lista para o informativo {#creating-a-list-for-the-newsletter}

Criar uma lista, por exemplo, **Informativo do Geometrixx**, no MCM para o boletim informativo ao qual as pessoas devem se inscrever. A criação de listas é descrita em [Criação de listas](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingnewlists).

O exemplo a seguir mostra uma lista:

![mcm_listcreate](assets/mcm_listcreate.png)

## Criar um formulário de inscrição {#create-a-sign-up-form}

Crie um formulário de registro de boletim informativo que permita que os usuários assinem tags. O site de exemplo do Geometrixx fornece uma página de informativo na barra de ferramentas do Geometrixx, onde você pode criar o formulário.

Para criar seu próprio formulário de informativo, consulte informações sobre a criação de formulários na [Documentação do Forms](/help/sites-authoring/default-components.md#form). O informativo usa as tags da Biblioteca de tags. Para adicionar tags adicionais, consulte [Administração de tags](/help/sites-authoring/tags.md#tagadministration).

Os campos ocultos no exemplo a seguir fornecem a quantidade mínima de informações (email); além disso, você pode adicionar mais campos posteriormente, mas isso afetará a taxa de conversão.

O exemplo a seguir é um formulário criado em https://localhost:4502/cf#/content/geometrixx/en/toolbar/newsletter.html.

1. Crie o formulário.

   ![mcm_newsletterpage](assets/mcm_newsletterpage.png)

1. Clique em **Editar** no componente Formulário para configurar o formulário para ir para uma página de agradecimento (consulte [Criando páginas de agradecimento](#creating-a-thank-you-page)).

   ![dc_formstart_thankyou](assets/dc_formstart_thankyou.png)

1. Defina a ação Formulário (isso é o que acontecerá quando você enviar o formulário) e configure o grupo para atribuir usuários registrados à lista criada anteriormente (por exemplo, geometrixx-newsletter).

   ![dc_formstart_thankyouadvanced](assets/dc_formstart_thankyouadvanced.png)

### Criando uma página de agradecimento {#creating-a-thank-you-page}

Quando os usuários clicarem em **Inscreva-se agora**, você deseja que a página Obrigado seja aberta automaticamente. Crie a página de agradecimento na página do informativo do Geometrixx. Depois de criar o formulário de informativo, edite o componente de Formulário e adicione o caminho à página de agradecimento.

O envio da solicitação leva o usuário a um **Obrigado** página após a qual receberão um email. Esta página de agradecimento foi criada em /content/geometrixx/en/toolbar/newsletter/thank_you.

![mcm_newsletter_thankyoupage](assets/mcm_newsletter_thankyoupage.png)

### Adicionar teasers {#adding-teasers}

Adicionar [teasers](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers) para direcionar públicos-alvo específicos. Por exemplo, você pode adicionar teasers à página de agradecimento e à página de cadastro da newsletter.

Para adicionar teasers para criar uma página de aterrissagem efetiva de boletim informativo:

1. Crie um parágrafo de teaser para um presente de inscrição. Selecionar **Primeiro** como estratégia e incluir um texto que informa qual presente eles receberão.

   ![dc_teaser_thankyou](assets/dc_teaser_thankyou.png)

1. Crie um parágrafo de teaser para a página de agradecimento. Selecionar **Primeiro** como estratégia e incluir texto que indica que o presente está a caminho.

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. Crie uma campanha com os dois teasers — marque um com business e outro sem tags.

### Envio de conteúdo aos assinantes {#pushing-content-to-subscribers}

Enviar quaisquer alterações para páginas por meio da funcionalidade Boletim informativo no MCM. Em seguida, você envia o conteúdo atualizado para os assinantes.

Consulte [Envio de informativos](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters).
