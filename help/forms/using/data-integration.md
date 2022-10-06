---
title: Integração de dados do AEM Forms
seo-title: AEM Forms Data Integration
description: A Integração de dados permite integrar o AEM Forms a diferentes fontes de dados e criar um modelo de dados de formulário para criar e trabalhar com formulários adaptáveis e comunicações interativas.
seo-description: Data Integration lets you integrate AEM Forms with disparate data sources and create form data model to create and work with adaptive forms and interactive communications.
uuid: 01df045e-1b26-437c-9674-fd223ecd5097
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: e397c6ce-d73f-4183-8445-1897a8906960
docset: aem65
feature: Form Data Model
exl-id: dd1146e4-952d-4dfa-8084-46c6096c4177
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# [!DNL AEM Forms] Integração de dados {#aem-forms-data-integration}

![](do-not-localize/data-integeration.png)

As infraestruturas empresariais incluem sistemas de back-end ou fontes de dados diferentes, como bancos de dados, serviços da Web, serviços REST, serviços OData e soluções CRM. Juntos, eles fazem um sistema de informações que fornece dados para aplicativos corporativos para executar negócios diários. Por outro lado, os aplicativos capturam dados e os enviam de volta para atualizar fontes de dados.

[!DNL AEM Forms] aplicativos como formulários adaptáveis e comunicações interativas exigem integração com fontes de dados para buscar dados do cliente enquanto renderiza formulários e cria comunicações interativas. Há casos de uso em que os dados são obtidos de fontes de dados com base em entradas de usuários em formulários adaptáveis. Além disso, os dados de formulário adaptável enviados podem ser gravados novamente para atualizar as respectivas fontes de dados.

Embora um sistema modular distribuído tenha seus próprios benefícios, o desafio é integrar e criar associações de dados em todas as fontes de dados. A integração de dados é a chave para uma infraestrutura empresarial funcional e eficiente, com diferentes fontes de dados conectadas a aplicativos para troca de dados comerciais.

## Visão geral da integração de dados {#data-integration-overview}

![aem-forms-data-integeration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] A integração de dados permite configurar e conectar diferentes fontes de dados com [!DNL AEM Forms]. Ele fornece uma interface de usuário intuitiva para criar um esquema de representação de dados unificado de entidades e serviços de negócios em fontes de dados conectadas. A representação unificada é conhecida como um modelo de dados de formulário, uma extensão do esquema JSON. As entidades em um modelo de dados de formulário são chamadas de objetos de modelo de dados. Um modelo de dados de formulário permite:

* Acesse objetos, propriedades e serviços do modelo de dados de fontes de dados conectadas.
* Criar objetos e propriedades personalizados do modelo de dados
* Criar associações entre objetos de modelo de dados dentro e entre fontes de dados.
* Chame os serviços de objeto do modelo de dados para consultar ou gravar dados de e para fontes de dados.

Depois de criar um modelo de dados de formulário, você pode usá-lo em vários workflows de comunicação adaptáveis e interativos, como:

* Criar formulários adaptáveis e comunicações interativas com base no modelo de dados de formulário
* Preencher previamente formulários adaptáveis e comunicações interativas a partir de fontes de dados configuradas
* Chamar serviços/operações de fonte de dados usando regras de formulário adaptáveis
* Gravar dados de formulário adaptável enviados em fontes de dados

## Introdução à integração de dados {#get-started-with-data-integration}

A primeira etapa para implementar a integração de dados é identificar e configurar fontes de dados que armazenam informações que você deseja aproveitar em formulários adaptáveis e casos de uso de comunicações interativas. Em seguida, crie um modelo de dados de formulário que use objetos, propriedades e serviços de modelo de dados de uma ou mais fontes de dados. É possível criar formulários adaptáveis e comunicações interativas com base em um modelo de dados de formulário em que os campos de formulário adaptável ou os espaços reservados em comunicações interativas estão vinculados às respectivas propriedades de fonte de dados.

[!DNL AEM Forms] O também permite criar um modelo de dados de formulário independente das fontes de dados e associar ou vincular objetos e propriedades do modelo de dados no modelo de dados de formulário à fonte de dados posteriormente. Ele elimina qualquer dependência das fontes de dados enquanto você trabalha em um modelo de dados de formulário.

Analise o seguinte para começar, entender e implementar a integração de dados.

* [Configurar fontes de dados](../../forms/using/configure-data-sources.md)
* [Criar modelo de dados de formulário](../../forms/using/create-form-data-models.md)
* [Trabalhar com o modelo de dados de formulário](../../forms/using/work-with-form-data-model.md)
* [Usar modelo de dados de formulário](../../forms/using/using-form-data-model.md)
