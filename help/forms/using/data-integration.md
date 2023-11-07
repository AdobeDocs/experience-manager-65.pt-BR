---
title: Integração de dados do AEM Forms
seo-title: AEM Forms Data Integration
description: A Integração de dados permite integrar o AEM Forms a fontes de dados diferentes e criar um modelo de dados de formulário para criar e trabalhar com formulários adaptáveis e comunicações interativas.
seo-description: Data Integration lets you integrate AEM Forms with disparate data sources and create form data model to create and work with adaptive forms and interactive communications.
uuid: 01df045e-1b26-437c-9674-fd223ecd5097
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: e397c6ce-d73f-4183-8445-1897a8906960
docset: aem65
feature: Form Data Model
exl-id: dd1146e4-952d-4dfa-8084-46c6096c4177
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# [!DNL AEM Forms] Integração de dados {#aem-forms-data-integration}

![hero-image](do-not-localize/data-integration.png)

As infraestruturas corporativas incluem sistemas back-end distintos ou fontes de dados como bancos de dados, serviços da Web, serviços REST, serviços OData e soluções de CRM. Juntas, elas fazem um sistema de informações que serve dados para aplicativos corporativos para realizar negócios diários. Por outro lado, os aplicativos capturam os dados e os enviam de volta para atualizar as fontes de dados.

[!DNL AEM Forms] aplicativos como formulários adaptáveis e comunicações interativas exigem integração com fontes de dados para buscar dados do cliente e, ao mesmo tempo, renderizar formulários e criar comunicações interativas. Há casos de uso em que os dados são obtidos de fontes de dados com base nas entradas do usuário em formulários adaptáveis. Além disso, os dados de formulário adaptável enviados podem ser gravados para atualizar as respectivas fontes de dados.

Embora um sistema modular e distribuído tenha seus próprios benefícios, o desafio está na integração e criação de associações de dados entre as fontes de dados. A integração de dados é a chave para uma infraestrutura empresarial funcional e eficiente, com diferentes fontes de dados conectadas a aplicativos para troca de dados de negócios.

## Visão geral da integração de dados {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] A Integração de dados permite configurar e conectar diferentes fontes de dados com o [!DNL AEM Forms]. Ele fornece uma interface de usuário intuitiva para criar um esquema de representação de dados unificada de entidades e serviços comerciais em fontes de dados conectadas. A representação unificada é conhecida como modelo de dados de formulário, uma extensão do esquema JSON. As entidades em um modelo de dados de formulário são chamadas de objetos do modelo de dados. Um modelo de dados de formulário permite:

* Acesse objetos de modelo de dados, propriedades e serviços a partir de fontes de dados conectadas.
* Criar objetos e propriedades de modelo de dados personalizados
* Crie associações entre objetos de modelo de dados em e entre fontes de dados.
* Invoque serviços de objeto de modelo de dados para consultar ou gravar dados de e para fontes de dados.

Depois de criar um modelo de dados de formulário, você pode usá-lo em vários formulários adaptáveis e workflows de comunicações interativas, como:

* Crie formulários adaptáveis e comunicações interativas com base no modelo de dados de formulário
* Preencher previamente os formulários adaptáveis e as comunicações interativas das fontes de dados configuradas
* Invocar serviços/operações de fonte de dados usando regras de formulário adaptáveis
* Gravar dados de formulário adaptável enviados nas fontes de dados

## Introdução à integração de dados {#get-started-with-data-integration}

A primeira etapa para implementar a integração de dados é identificar e configurar fontes de dados que armazenam informações que você deseja usar em formulários adaptáveis e casos de uso de comunicações interativas. Em seguida, crie um modelo de dados de formulário que use o objeto de modelo de dados, as propriedades e os serviços de uma ou mais fontes de dados. Você pode criar formulários adaptáveis e comunicações interativas com base em um modelo de dados de formulário em que os campos de formulário adaptáveis ou espaços reservados em comunicações interativas são vinculados às respectivas propriedades da fonte de dados.

[!DNL AEM Forms] também permite criar um modelo de dados de formulário independente das fontes de dados e associar ou vincular objetos de modelo de dados e propriedades no modelo de dados de formulário com a fonte de dados posteriormente. Ele elimina qualquer dependência em fontes de dados enquanto você trabalha em um modelo de dados de formulário.

Analise o seguinte para começar, entender e implementar a integração de dados.

* [Configurar fontes de dados](../../forms/using/configure-data-sources.md)
* [Criar modelo de dados de formulário](../../forms/using/create-form-data-models.md)
* [Trabalhar com o modelo de dados de formulário](../../forms/using/work-with-form-data-model.md)
* [Usar modelo de dados de formulário](../../forms/using/using-form-data-model.md)
