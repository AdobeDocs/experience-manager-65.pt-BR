---
title: Tutorial - Criar sua primeira comunicação interativa
seo-title: Criar sua primeira comunicação interativa
description: Saiba como criar sua primeira Comunicação interativa.
seo-description: Saiba como criar sua primeira Comunicação interativa.
uuid: ed5003c6-ba3a-4fcb-8645-c7b607b22fb5
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
discoiquuid: 954da8da-a30b-477d-bde7-3edd86a5be11
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 0%

---


# Tutorial: Criar sua primeira comunicação interativa {#tutorial-create-your-first-interactive-communication}

Saiba como criar sua primeira Comunicação interativa.

![01-create-first-adaptive-form-herói-image](assets/01-create-first-adaptive-form-hero-image.png)

O Interative Communications centraliza e gerencia a criação, montagem e delivery de correspondências seguras, personalizadas e interativas, como correspondência comercial, documentos, declarações, emails de marketing, contas e kits de boas-vindas. As Comunicações interativas podem ser entregues usando dois canais: Imprimir e Web. O canal Print é usado para criar PDFs e comunicações em papel, enquanto o canal da Web é usado para fornecer experiências online.

Este tutorial fornece uma estrutura completa para criar uma comunicação interativa. O tutorial é organizado em um caso de uso e em várias guias. Cada guia ajuda a criar recursos que são usados como blocos de construção para criar uma Comunicação interativa.

A imagem a seguir ilustra os blocos de construção necessários para criar uma comunicação interativa.

![fluxo de trabalho](assets/workflow.gif)

No final deste tutorial, você poderá:

* Criar blocos de construção (modelo de dados de formulário, fragmentos de documento e modelos)
* Criar uma comunicação interativa
* Testar e publicar uma comunicação interativa

## Use case {#use-case}

A jornada start com o aprendizado do caso de uso:

Um operador de telecom envia contas mensais aos clientes por email. O projeto de lei é uma Comunicação Interativa. O email inclui:

* Um PDF protegido por senha, conhecido como canal de impressão neste tutorial. Inclui detalhes do cliente, detalhes da lista, resumo das cobranças, modos convenientes de pagamento da lista e detalhes de uso.
* Um link para a versão da Web da lista, conhecido como canal da Web neste tutorial. A versão da Web da lista, além dos detalhes abordados na versão PDF, fornece uma representação gráfica dos detalhes de uso e ofertas personalizadas com base no Adobe Target. A versão da Web também contém um formulário de pagamento on-line. Ajuda a efetuar pagamentos em linha sem deixar o IC.
* Um link para serviços de valor agregado, como armazenamento online, subscrições de música e subscrições de vídeo sob demanda.

## Pré-requisitos {#prerequisites}

* Configure uma instância do autor AEM.
* Instalar complemento [do](/help/forms/using/installing-configuring-aem-forms-osgi.md) AEM Forms na instância do autor
* Configurar o banco de dados MYSQL
* Obtenha o driver de banco de dados JDBC (arquivo JAR) do provedor de banco de dados. Os exemplos no tutorial são baseados no banco de dados MySQL e usam o driver [de banco de dados](https://dev.mysql.com/downloads/connector/j/5.1.html)MySQL JDBC da Oracle.

## Etapa 1: Planeje a comunicação interativa {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

A primeira etapa no planejamento de uma comunicação interativa é finalizar o conteúdo da comunicação interativa. Após a finalização do conteúdo, é necessário analisá-lo para identificar os vários tipos de ativos necessários para criar a Comunicação interativa.

**Objetivos:**

Para criar uma anatomia para a Comunicação interativa com os seguintes modos de entrada de dados:

* Texto estático
* Modelo de dados de formulário
* IU do agente
* Dados condicionais
* Imagens

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/planning-interactive-communications.md)

## Step 2: Create form data model {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Um modelo de dados de formulário permite que você conecte uma Comunicação interativa a fontes de dados diferentes. Por exemplo, AEM perfil do usuário, serviços Web RESTful, serviços Web baseados em SOAP, serviços OData e bancos de dados relacionais. Um modelo de dados de formulário é um schema unificado de representação de dados de entidades de negócios e serviços disponíveis em fontes de dados conectadas. Você pode usar o modelo de dados de formulário com uma Comunicação Interativa para recuperar dados de fontes de dados conectadas. Para obter mais informações sobre o modelo de dados de formulário, consulte Integração [de dados da](/help/forms/using/data-integration.md)AEM Forms.

**Objetivos:**

* Configurar a instância do banco de dados (banco de dados MySQL) como uma fonte de dados
* Criar o modelo de dados de formulário usando o banco de dados MySQL como uma fonte de dados
* Adicionar objetos de modelo de dados ao modelo de dados de formulário
* Configurar serviços de leitura e gravação para o modelo de dados de formulário
* Criar associações entre objetos de modelo de dados
* Visualização de dados de amostra gerados automaticamente
* Editar dados de amostra
* Testar modelo de dados de formulário e serviços configurados com dados de teste

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-form-data-model0.md)

## Etapa 3: Criar fragmentos de documento {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Os fragmentos de documento são componentes reutilizáveis de uma correspondência que são usados para compor uma comunicação interativa. Os fragmentos do documento são de tipos: Texto, Lista e Condição.

**Objetivos:**

* Criar fragmentos de documento
* Criar variáveis
* Criar e aplicar regras

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-document-fragments.md)

## Etapa 4: Criar modelos {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Para criar uma comunicação interativa, você deve ter modelos disponíveis no servidor AEM para Canais de impressão e da Web.

Os modelos para o canal Imprimir são criados no Adobe Forms Designer e carregados no servidor AEM. Esses modelos ficam disponíveis para uso ao criar uma Comunicação interativa.

Os modelos para o canal da Web são criados no AEM. Os autores e administradores de modelos podem criar, editar e ativar modelos da Web. Depois de criados e ativados, esses modelos ficam disponíveis para uso ao criar uma Comunicação interativa.

**Objetivos:**

* Criar modelos XDP para canal de impressão usando o Adobe Forms Designer
* Carregar os modelos XDP no AEM Forms Server
* Criar e ativar modelos para o canal da Web

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-templates-print-web.md)

## Etapa 5: Criar uma comunicação interativa {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Depois de criar todos os blocos de construção, como modelo de dados de formulário, fragmentos de documento e modelos para a versão da Web, você pode criar um start para a criação de uma comunicação interativa.

As Comunicações interativas podem ser fornecidas por meio de dois canais: Imprimir e Web. Você também pode criar um canal de comunicação interativa com impressão como o principal. A opção Imprimir como principal para o canal da Web garante que o conteúdo, a herança e o vínculo de dados do canal da Web sejam derivados do canal Imprimir.

**Objetivos:**

* Criar comunicação interativa para o canal de impressão
* Criar comunicação interativa para o canal da Web
* Crie Comunicações interativas da Web e da impressão com a opção Imprimir como Principal
* Criar uma tabela dinâmica na versão Web do Interative Communication
* Criar um gráfico na versão Web do Interative Communication
* Criar hiperlinks na versão da Web do Interative Communication

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-interactive-communication0.md)

## Etapa 6: Testar sua comunicação interativa {#step-test-your-interactive-communication}

![11-teste-sua-forma adaptativa](assets/11-test-your-adaptive-form.png)

Depois de criar uma Comunicação interativa, é importante testar todas as alterações feitas nelas. Testar cada campo de uma comunicação interativa é tedioso. A AEM Forms fornece um SDK (Calvin SDK) para automatizar o teste de Comunicações interativas no navegador da Web.

**Objetivos:**

* Criar conjunto de testes
* Criar casos de teste
* Execute os casos de teste

## Etapa 7: Publicar sua comunicação interativa {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

Depois de criar e testar o Interative Communications usando canais de Impressão e da Web, você pode publicar esses ativos. O caso de uso descrito neste tutorial foca na integração desses ativos com um cliente de email. O cliente de email serve como uma ponte para enviar as Comunicações interativas para vários endereços de email.

**Objetivos:**

* Integre o Interative Communications a um cliente de email para poder enviar uma comunicação aos clientes
* Incluir um documento PDF como anexo (Comunicação interativa criada no canal de impressão)
* Incluir um link para a versão da Web do Interative Communication

