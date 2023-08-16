---
title: Tutorial - Criar a primeira comunicação interativa
seo-title: Create your first Interactive Communication
description: Saiba como criar sua primeira Comunicação interativa.
seo-description: Learn to create your first Interactive Communication.
uuid: ed5003c6-ba3a-4fcb-8645-c7b607b22fb5
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
discoiquuid: 954da8da-a30b-477d-bde7-3edd86a5be11
feature: Interactive Communication
exl-id: b20bb719-5686-466e-8dde-279b8471bfe3
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 1%

---

# Tutorial: criar a primeira comunicação interativa {#tutorial-create-your-first-interactive-communication}

Saiba como criar sua primeira Comunicação interativa.

![01-criar-primeiro-formulário-adaptável-imagem-herói](assets/01-create-first-adaptive-form-hero-image.png)

As Comunicações interativas centralizam e gerenciam a criação, montagem e delivery de correspondências seguras, personalizadas e interativas, como correspondência comercial, documentos, declarações, emails de marketing, contas e kits de boas-vindas. As Comunicações interativas podem ser fornecidas usando dois canais: Impressão e Web. O canal de impressão é usado para criar PDF e comunicações em papel, enquanto o canal da Web é usado para oferecer experiências online.

Este tutorial fornece uma estrutura completa para criar uma comunicação interativa. O tutorial é organizado em um caso de uso e em vários guias. Cada guia ajuda a criar recursos que são usados como blocos de construção para criar uma Comunicação interativa.

A imagem a seguir ilustra os elementos essenciais necessários para criar uma comunicação interativa.

![fluxo de trabalho](assets/workflow.gif)

Ao final deste tutorial, você será capaz de:

* Criar blocos de construção (modelo de dados de formulário, fragmentos de documento e modelos)
* Criar uma comunicação interativa
* Testar e publicar uma comunicação interativa

## Caso de uso {#use-case}

A jornada começa aprendendo o caso de uso:

Uma operadora de telecomunicações envia faturas mensais aos clientes por email. A lei é uma comunicação interativa. O e-mail inclui:

* Um PDF protegido por senha, conhecido como Canal de impressão neste tutorial. Inclui detalhes do cliente, detalhes da fatura, sumário de encargos, modos convenientes de pagamento da fatura e detalhes de uso.
* Um link para a versão da lista da Web, conhecido como canal da Web neste tutorial. A versão da conta na web, além dos detalhes abordados na versão PDF, fornece uma representação gráfica dos detalhes de uso e ofertas personalizadas com base no Adobe Target. A versão da Web também contém um formulário de pagamento online. Ajuda a fazer pagamentos on-line sem sair da IC.
* Um link para serviços de valor agregado, como armazenamento online, assinaturas de música e assinaturas de vídeo sob demanda.

## Pré-requisitos {#prerequisites}

* Configure uma instância de autor do AEM.
* Instalar [Complemento do AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) na instância do autor
* Configurar o banco de dados MYSQL
* Obter o driver de banco de dados JDBC (arquivo JAR) do provedor de banco de dados. Exemplos no tutorial são baseados no banco de dados MySQL e usam o Oracle [Driver de banco de dados JDBC MySQL](https://dev.mysql.com/downloads/connector/j/5.1.html).

## Etapa 1: Planejar a comunicação interativa {#step-plan-the-interactive-communication}

![07-aplicar-regras-ao-formulário-adaptável_pequeno](assets/07-apply-rules-to-adaptive-form_small.png)

A primeira etapa no planejamento de uma comunicação interativa é finalizar o conteúdo da comunicação interativa. Depois que o conteúdo for finalizado, você deverá analisá-lo para identificar os vários tipos de ativos necessários para criar a Comunicação interativa.

**Metas:**

Para criar uma anatomia para a Comunicação interativa com os seguintes modos de entrada de dados:

* Texto estático
* Modelo de dados do formulário
* IU do agente
* Dados condicionais
* Imagens

[](/help/forms/using/planning-interactive-communications.md)

## Etapa 2: Criar modelo de dados de formulário {#step-create-form-data-model}

![03-criar-formulário-adaptável-imagem-principal_pequeno](assets/03-create-adaptive-form-main-image_small.png)

Um modelo de dados de formulário permite conectar uma Comunicação interativa a fontes de dados diferentes. Por exemplo, perfil de usuário AEM, serviços Web RESTful, serviços Web baseados em SOAP, serviços OData e bancos de dados relacionais. Um modelo de dados de formulário é um esquema de representação de dados unificada de entidades e serviços comerciais disponíveis em fontes de dados conectadas. Você pode usar o modelo de dados de formulário com uma Comunicação interativa para recuperar dados de fontes de dados conectadas. Para obter mais informações sobre o modelo de dados de formulário, consulte [Integração de dados do AEM Forms](/help/forms/using/data-integration.md).

**Metas:**

* Configurar a instância do banco de dados (banco de dados MySQL) como uma fonte de dados
* Criar o modelo de dados de formulário usando o banco de dados MySQL como uma fonte de dados
* Adicionar objetos de modelo de dados ao modelo de dados de formulário
* Configurar serviços de leitura e gravação para o modelo de dados de formulário
* Criar associações entre os objetos de modelo de dados
* Exibir dados de amostra gerados automaticamente
* Editar dados de amostra
* Testar o modelo de dados do formulário e os serviços configurados com dados de teste

[](/help/forms/using/create-form-data-model0.md)

## Etapa 3: Criar fragmentos de documento {#step-create-document-fragments}

![05-criar-formulário-modelo-dados-principal_pequeno](assets/05-create-form-data-model-main_small.png)

Os fragmentos de documento são componentes reutilizáveis de uma correspondência usados para compor uma comunicação interativa. Os fragmentos de documento são dos tipos: Texto, Lista e Condição.

**Metas:**

* Criar fragmentos de documento
* Criar variáveis
* Criar e aplicar regras

[](/help/forms/using/create-document-fragments.md)

## Etapa 4: criar modelos {#step-create-templates}

![07-aplicar-regras-ao-formulário-adaptável_pequeno](assets/07-apply-rules-to-adaptive-form_small.png)

Para criar uma comunicação interativa, você deve ter modelos disponíveis no servidor AEM para impressão e canais da Web.

Os modelos para o canal de impressão são criados no Adobe Forms Designer e carregados no servidor AEM. Esses modelos ficam disponíveis para uso ao criar uma Comunicação interativa.

Os templates para o canal da Web são criados no AEM. Os autores e administradores de modelos podem criar, editar e ativar modelos da Web. Depois de criados e ativados, esses modelos ficam disponíveis para uso ao criar uma Comunicação interativa.

**Metas:**

* Criar modelos XDP para canal de impressão usando o Adobe Forms Designer
* Fazer upload dos modelos XDP para o servidor do AEM Forms
* Criar e habilitar modelos para o canal da Web

[](/help/forms/using/create-templates-print-web.md)

## Etapa 5: Criar uma comunicação interativa {#step-create-an-interactive-communication}

![09-estilo-seu-formulário-adaptável-pequeno](assets/09-style-your-adaptive-form-small.png)

Depois de criar todos os blocos de construção, como modelo de dados de formulário, fragmentos de documento e modelos para a versão da Web, você pode começar a criar uma comunicação interativa.

As Comunicações interativas podem ser fornecidas por meio de dois canais: Impressão e Web. Você também pode criar uma Comunicação interativa com o canal de impressão como mestre. A opção Print as master para o canal da Web garante que o conteúdo, a herança e a associação de dados do canal da Web sejam derivados do canal de impressão.

**Metas:**

* Criar comunicação interativa para o canal de impressão
* Criar comunicação interativa para o canal da Web
* Criar comunicações interativas da Web e de impressão com Imprimir como mestre
* Criar uma tabela dinâmica na versão da Web da Comunicação interativa
* Criar um gráfico na versão da Web da Comunicação Interativa
* Criar hiperlinks na versão da Web da comunicação interativa

[](/help/forms/using/create-interactive-communication0.md)

## Etapa 6: publicar a comunicação interativa {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-small](assets/12-publish-your-adaptive-form-_small.png)

Depois de criar e testar as Comunicações interativas usando canais de impressão e da Web, você poderá publicar esses ativos. O caso de uso descrito neste tutorial foca na integração desses ativos com um cliente de email. O cliente de email serve como uma ponte para enviar as Comunicações interativas para vários endereços de email.

**Metas:**

* Integre as Comunicações interativas a um cliente de email para poder enviar uma comunicação aos clientes
* Incluir um documento PDF como anexo (Comunicação interativa criada no canal de impressão)
* Incluir um link para a versão da Web da comunicação interativa
