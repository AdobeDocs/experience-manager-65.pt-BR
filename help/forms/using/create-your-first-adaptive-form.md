---
title: '"Tutorial: Criar o primeiro formulário adaptável"'
seo-title: '"Tutorial: Criar o primeiro formulário adaptável"'
description: Saiba como criar formulários de classe empresarial, interativos e responsivos.
seo-description: Saiba como criar formulários de classe empresarial, interativos e responsivos.
uuid: ee351a3f-ea6a-4b4c-8045-4948ad51b7c1
topic-tags: introduction
discoiquuid: 1142bcd4-e3a7-41ce-a710-132ae6c21dbe
docset: aem65
feature: Formulários adaptáveis
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---


# Tutorial: Crie seu primeiro formulário adaptável {#tutorial-create-your-first-adaptive-form}

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## Introdução {#introduction}

Você está procurando uma **experiência de formulários para dispositivos móveis** que simplifique a inscrição, aumente o engajamento e reduza o tempo de resposta, **formulários adaptáveis** é uma opção perfeita para você. Os formulários adaptáveis oferecem uma experiência de formulários móveis, automatizada e compatível com análises. É possível criar facilmente formulários responsivos e interativos por natureza, usar processos automatizados para reduzir tarefas administrativas e repetitivas e usar a análise de dados para melhorar e personalizar a experiência que os clientes têm com seus formulários.

Este tutorial fornece uma estrutura completa para criar um formulário adaptável. O tutorial é organizado em um caso de uso e vários guias. Cada guia ajuda você a aprender e adicionar novos recursos ao formulário adaptável criado neste tutorial. Você tem um formulário adaptável em funcionamento após cada guia. O guia para criar um formulário adaptável está disponível. Os guias subsequentes estarão disponíveis em breve. Ao final deste tutorial, você poderá:

* Crie um formulário adaptável e um modelo de dados de formulário.
* Estilo do formulário adaptável.
* Use o editor de regras de formulário adaptável para criar regras de negócios.
* Teste e publique um formulário adaptável.

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

A jornada começa com o aprendizado do caso de uso:

Um site da Web oferece uma variedade de produtos para diversos clientes. Os clientes navegam pelo portal, selecionam e solicitam os produtos. Cada cliente cria uma conta e fornece endereços de envio e faturamento. Uma cliente já existente, Sara Rose, está procurando adicionar seu endereço de envio ao site. O site fornece um formulário online para adicionar e atualizar endereços de envio.

O site é executado no Adobe Experience Manager (AEM) e usa AEM [!DNL Forms] para captura e processamento de dados. O formulário de adição e atualização de endereço é um formulário adaptável. O site armazena os detalhes do cliente em um banco de dados. Eles usam o formulário de adição e atualização de endereço para recuperar e exibir os endereços disponíveis. Eles também usam o formulário adaptável para aceitar endereços atualizados e novos.

### Pré-requisitos {#prerequisite}

* Configure uma instância do autor de AEM.
* Instale o [complemento AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md) na instância do autor.
* Obtenha o driver de banco de dados JDBC (arquivo JAR) do provedor de banco de dados. Os exemplos no tutorial são baseados no banco de dados [!DNL MySQL] e usam [!DNL Oracle's] [driver de banco de dados JDBC MySQL](https://dev.mysql.com/downloads/connector/j/5.1.html).

* Configure um banco de dados contendo dados do cliente com os campos exibidos abaixo. Um banco de dados não é essencial para criar um formulário adaptável. Este tutorial usa um banco de dados para exibir o modelo de dados de formulário e os recursos de persistência de AEM [!DNL Forms].

![adaptiveformdata](assets/adaptiveformdata.png)

## Etapa 1: Criar um formulário adaptável {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Os formulários adaptáveis são de nova geração, envolvente, responsivo, dinâmico e adaptável por natureza. Usando formulários adaptáveis, você pode fornecer experiências personalizadas e direcionadas. AEM [!DNL Forms] fornece um editor WYSIWYG de arrastar e soltar para criar formulários adaptáveis. Para obter mais informações sobre formulários adaptáveis, consulte [Introdução à criação de formulários adaptáveis](../../forms/using/introduction-forms-authoring.md).

Metas:

* Crie um formulário adaptável que permita ao cliente adicionar um endereço de envio
* Campos de layout de um formulário adaptável para exibir e aceitar informações de um cliente
* Criar ação de envio para enviar um email contendo conteúdo de formulário
* Visualizar e enviar um formulário adaptável

[![Consulte o Guia](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## Etapa 2: Criar Modelo de Dados de Formulário {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Um modelo de dados de formulário permite conectar um formulário adaptável a diferentes fontes de dados. Por exemplo, AEM perfil de usuário, serviços da Web RESTful, serviços da Web baseados em SOAP, serviços OData e bancos de dados relacionais. Um modelo de dados de formulário é um esquema de representação de dados unificado de entidades comerciais e serviços disponíveis em fontes de dados conectadas. É possível usar o modelo de dados de formulário com um formulário adaptável para recuperar, atualizar, excluir e adicionar dados a fontes de dados conectadas.

Metas:

* Configurar a instância do banco de dados do site (banco de dados [!DNL MySQL]) como fontes de dados
* Criar o modelo de dados de formulário usando o banco de dados [!DNL MySQL] como uma fonte de dados
* Adicionar objetos de modelo de dados ao modelo de dados de formulário
* Configurar serviços de leitura e gravação para o modelo de dados de formulário
* Testar modelo de dados de formulário e serviços configurados com dados de teste

[![Consulte o Guia](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## Etapa 3: Aplicar regras a campos de formulário adaptáveis {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Os formulários adaptáveis fornecem um editor para gravar regras em objetos de formulário adaptáveis. Essas regras definem ações a serem acionadas em objetos de formulário com base em condições predefinidas, entradas de usuário e ações de usuário no formulário. Ele ajuda a garantir a precisão e acelera a experiência de preenchimento de formulários.

Metas:

* Criar e aplicar regras a campos de formulário adaptáveis
* Usar regras para acionar serviços de modelo de dados de formulário para atualizar dados para o banco de dados

[![Consulte o Guia](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## Etapa 4: Estilo do formulário adaptável {#step-style-your-adaptive-form}

![](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

Os formulários adaptáveis fornecem temas e um [editor](../../forms/using/themes.md) para criar temas para os formulários adaptáveis. Um tema contém detalhes de estilo para componentes e painéis, e você pode reutilizar um tema em diferentes formas. Os estilos incluem propriedades como cores de plano de fundo, cores de estado, transparência, alinhamento e tamanho. Quando o tema é aplicado ao formulário, o estilo especificado reflete nos componentes correspondentes do formulário. Formulários adaptáveis também oferecem suporte ao estilo em linha para estilos específicos de um formulário.

Metas:

* Aplicar um tema pronto para uso a um formulário adaptável
* Criar um tema para um formulário adaptável usando o editor de temas
* Usar fontes da Web em um tema personalizado

[![Consulte o Guia](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## Etapa 5: Teste seu formulário adaptável {#step-test-your-adaptive-form}

![11-teste-o-formulário adaptável](assets/11-test-your-adaptive-form.png)

Os formulários adaptáveis são parte integrante das interações do cliente. É importante testar seus formulários adaptáveis com todas as alterações feitas neles. Testar cada campo de um formulário é entediante. AEM [!DNL Forms] fornece um SDK (Calvin SDK) para automatizar o teste de formulários adaptáveis. O Calvin permite automatizar o teste de seus formulários adaptáveis no navegador da Web.

Metas:

* Criar conjunto de teste para o formulário adaptável
* Criar casos de teste para formulários adaptáveis
* Executar os casos de teste

[![Consulte o Guia](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](testing-your-adaptive-form.md)

## Etapa 6: Publicar o formulário adaptável {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

Você pode publicar formulários adaptáveis como um formulário independente (aplicativo de página única), incluir AEM [página Sites](/help/forms/using/embed-adaptive-form-aem-sites.md) ou listar em um AEM [!DNL Site] usando [Forms Portal](../../forms/using/introduction-publishing-forms.md).

Metas:

* Publicar o formulário adaptável como uma página de AEM
* Incorpore o formulário adaptável em uma página AEM [!DNL Sites]
* Incorporar o formulário adaptável em uma página da Web externa (uma página da Web que não seja AEM hospedada fora do AEM)

[![Consulte o Guia](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)