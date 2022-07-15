---
title: Tutorial - Criar sua primeira comunicação interativa
seo-title: Create your first Interactive Communication
description: Saiba como criar sua primeira comunicação interativa.
seo-description: Learn to create your first Interactive Communication.
uuid: ed5003c6-ba3a-4fcb-8645-c7b607b22fb5
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
discoiquuid: 954da8da-a30b-477d-bde7-3edd86a5be11
feature: Interactive Communication
exl-id: b20bb719-5686-466e-8dde-279b8471bfe3
source-git-commit: 471d7f48dc4653000b4852dbbeb886b05e28e644
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 1%

---

# Tutorial: Criar sua primeira comunicação interativa {#tutorial-create-your-first-interactive-communication}

Saiba como criar sua primeira comunicação interativa.

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

As Comunicações interativas centralizam e gerenciam a criação, montagem e delivery de correspondências seguras, personalizadas e interativas, como correspondência comercial, documentos, declarações, emails de marketing, contas e kits de boas-vindas. As Comunicações interativas podem ser entregues usando dois canais: Imprimir e Web. O canal Imprimir é usado para criar PDF e comunicações em papel, enquanto o canal Web é usado para fornecer experiências online.

Este tutorial fornece uma estrutura completa para criar uma Comunicação interativa. O tutorial é organizado em um caso de uso e vários guias. Cada guia ajuda você a criar recursos que são usados como blocos de construção para criar uma Comunicação interativa.

A imagem a seguir ilustra os blocos fundamentais necessários para criar uma Comunicação interativa.

![fluxo de trabalho](assets/workflow.gif)

Ao final deste tutorial, você poderá:

* Criar blocos de construção (modelo de dados de formulário, fragmentos de documento e modelos)
* Criar uma comunicação interativa
* Testar e publicar uma comunicação interativa

## Caso de uso {#use-case}

A jornada começa com o aprendizado do caso de uso:

Um operador de telecom envia contas mensais para os clientes por email. A lista é uma Comunicação Interativa. O email inclui:

* Um PDF protegido por senha, conhecido como Canal de impressão neste tutorial. Ele inclui detalhes do cliente, detalhes da lista, resumo dos encargos, modos convenientes de pagamento da fatura e detalhes de uso.
* Um link para a versão da Web do bill, conhecido como canal da Web neste tutorial. A versão da web da fatura, além dos detalhes abordados na versão do PDF, fornece uma representação gráfica dos detalhes de uso e das ofertas personalizadas com base no Adobe Target. A versão web também contém um formulário de pagamento online. Ajuda a efetuar pagamentos em linha sem sair do IC.
* Um link para serviços de valor agregado, como armazenamento online, assinaturas de música e assinaturas de vídeo sob demanda.

## Pré-requisitos {#prerequisites}

* Configure uma instância do autor de AEM.
* Instalar [Complemento do AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) na instância do autor
* Configurar o banco de dados MYSQL
* Obtenha o driver de banco de dados JDBC (arquivo JAR) do provedor de banco de dados. Os exemplos no tutorial são baseados no banco de dados MySQL e usam o Oracle [Driver de banco de dados JDBC do MySQL](https://dev.mysql.com/downloads/connector/j/5.1.html).

## Etapa 1: Planejar a comunicação interativa {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

A primeira etapa no planejamento de uma comunicação interativa é finalizar o conteúdo da comunicação interativa. Após a finalização do conteúdo, é necessário analisá-lo para identificar os vários tipos de ativos necessários para criar a Comunicação interativa.

**Metas:**

Para criar uma anatomia para a Comunicação interativa com os seguintes modos de entrada de dados:

* Texto estático
* Modelo de dados do formulário
* IU do agente
* Dados condicionais
* Imagens

[ ](/help/forms/using/planning-interactive-communications.md)

## Etapa 2: Criar modelo de dados de formulário {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Um modelo de dados de formulário permite conectar uma Comunicação interativa a diferentes fontes de dados. Por exemplo, AEM perfil de usuário, serviços da Web RESTful, serviços da Web baseados em SOAP, serviços OData e bancos de dados relacionais. Um modelo de dados de formulário é um esquema de representação de dados unificado de entidades comerciais e serviços disponíveis em fontes de dados conectadas. Você pode usar o modelo de dados de formulário com uma Comunicação interativa para recuperar dados de fontes de dados conectadas. Para obter mais informações sobre o modelo de dados de formulário, consulte [Integração de dados do AEM Forms](/help/forms/using/data-integration.md).

**Metas:**

* Configurar instância de banco de dados (banco de dados MySQL) como fonte de dados
* Criar o modelo de dados de formulário usando o banco de dados MySQL como uma fonte de dados
* Adicionar objetos de modelo de dados ao modelo de dados de formulário
* Configurar serviços de leitura e gravação para o modelo de dados de formulário
* Criar associações entre os objetos do modelo de dados
* Exibir dados de amostra gerados automaticamente
* Editar dados de amostra
* Testar modelo de dados de formulário e serviços configurados com dados de teste

[ ](/help/forms/using/create-form-data-model0.md)

## Etapa 3: Criar fragmentos de documento {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Fragmentos de documento são componentes reutilizáveis de uma correspondência usados para compor uma Comunicação interativa. Os fragmentos de documento são dos tipos: Texto, Lista e Condição.

**Metas:**

* Criar fragmentos de documento
* Criar variáveis
* Criar e aplicar regras

[ ](/help/forms/using/create-document-fragments.md)

## Etapa 4: Criar modelos {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Para criar uma Comunicação interativa, você deve ter modelos disponíveis no servidor de AEM para Canais de impressão e da Web.

Os modelos para o canal de impressão são criados no Adobe Forms Designer e carregados no servidor de AEM. Esses modelos ficam disponíveis para uso ao criar uma Comunicação interativa.

Os modelos para o canal Web são criados em AEM. Os autores e administradores de modelos podem criar, editar e ativar modelos da Web. Depois de criados e ativados, esses modelos estão disponíveis para uso ao criar uma Comunicação interativa.

**Metas:**

* Criar modelos XDP para canal de impressão usando o Adobe Forms Designer
* Fazer upload dos modelos XDP no servidor do AEM Forms
* Criar e ativar modelos para o canal Web

[ ](/help/forms/using/create-templates-print-web.md)

## Etapa 5: Criar uma comunicação interativa {#step-create-an-interactive-communication}

![Estilo 09-o-forma adaptável-pequena](assets/09-style-your-adaptive-form-small.png)

Depois de criar todos os blocos de construção, como modelo de dados de formulário, fragmentos de documento e modelos para a versão da Web, você pode começar a criar uma Comunicação interativa.

As Comunicações interativas podem ser entregues por meio de dois canais: Imprimir e Web. Você também pode criar um canal de Comunicação interativa com impressão como o principal. A opção Imprimir como principal para canal da Web garante que o conteúdo, a herança e o vínculo de dados do canal da Web sejam derivados do canal Imprimir.

**Metas:**

* Criar comunicação interativa para o canal de impressão
* Criar comunicação interativa para o canal da Web
* Crie Comunicações Interativas da Web e Imprimir como Principal
* Criar uma tabela dinâmica na versão da Web da Comunicação interativa
* Criar um gráfico na versão Web da Comunicação interativa
* Criar hiperlinks na versão da Web da Comunicação interativa

[ ](/help/forms/using/create-interactive-communication0.md)

## Etapa 6: Publicar sua comunicação interativa {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

Depois de criar e testar as Comunicações interativas usando os canais Imprimir e Web, você pode publicar esses ativos. O caso de uso descrito neste tutorial tem como foco a integração desses ativos com um cliente de email. O cliente de email serve como uma ponte para enviar as Comunicações interativas para vários endereços de email.

**Metas:**

* Integre as Comunicações interativas a um cliente de email para poder enviar uma comunicação para os clientes
* Incluir um documento PDF como anexo (Comunicação interativa criada no canal de impressão)
* Incluir um link para a versão da Web da Comunicação interativa
