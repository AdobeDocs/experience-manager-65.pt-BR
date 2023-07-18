---
title: "Tutorial: Criar o primeiro formulário adaptável"
seo-title: "Tutorial: Create your first adaptive form"
description: Saiba como criar formulários empresariais, interativos e responsivos.
seo-description: Learn to create business class, interactive, and responsive forms.
uuid: ee351a3f-ea6a-4b4c-8045-4948ad51b7c1
topic-tags: introduction
discoiquuid: 1142bcd4-e3a7-41ce-a710-132ae6c21dbe
docset: aem65
feature: Adaptive Forms
exl-id: 77a05f83-ac9a-4221-85ac-439e82623a28
source-git-commit: 1683338f02d01d5d9843368955fa42f309718f26
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 11%

---

# Tutorial: criar o primeiro formulário adaptável {#tutorial-create-your-first-adaptive-form}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=pt-br) |
| AEM 6.5 | Este artigo |


![01-criar-primeiro-formulário-adaptável-imagem-herói](assets/01-create-first-adaptive-form-hero-image.png)

## Introdução {#introduction}

Você está procurando um **experiência de formulários** que simplifica a inscrição, aumenta o engajamento e reduz o tempo de retorno, **formulários adaptáveis** O é o ajuste perfeito para você. Os formulários adaptáveis fornecem uma experiência em formulários móveis, de automação e compatíveis com a análise. Você pode criar facilmente formulários responsivos e interativos por natureza, usar processos automatizados para reduzir tarefas administrativas e repetitivas e usar a análise de dados para melhorar e personalizar a experiência que os clientes têm com seus formulários.

Este tutorial fornece uma estrutura completa para criar um formulário adaptável. O tutorial é organizado em um caso de uso e em vários guias. Cada guia ajuda você a conhecer e adicionar novos recursos ao formulário adaptável criado neste tutorial. Você tem um formulário adaptável de trabalho depois de cada guia. O guia para criar um formulário adaptável está disponível. Os guias subsequentes estarão disponíveis em breve. Ao final deste tutorial, você será capaz de:

* Crie um formulário adaptável e um modelo de dados de formulário.
* Estilize o formulário adaptável.
* Use o editor de regras de formulário adaptável para criar regras de negócios.
* Teste e publique um formulário adaptável.

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

A jornada começa aprendendo o caso de uso:

Um site oferece uma variedade de produtos para clientes diversos. Os clientes navegam pelo portal, selecionam e solicitam os produtos. Cada cliente cria uma conta e fornece endereços de entrega e cobrança. Uma cliente existente, Sara Rose, está procurando adicionar seu endereço de entrega ao site. O site fornece um formulário online para adicionar e atualizar endereços de envio.

O site é executado no Adobe Experience Manager (AEM) e usa AEM [!DNL Forms] para captura e processamento de dados. O formulário de adição e atualização de endereço é um formulário adaptável. O site armazena os detalhes do cliente em um banco de dados. Eles usam o formulário de adição e atualização de endereço para recuperar e exibir os endereços disponíveis. Eles também usam o formulário adaptável para aceitar endereços atualizados e novos.

### Pré-requisitos {#prerequisite}

* Configurar um [Instância de autor AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#author-and-publish-installs)
* Instalar [Complemento do AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md) na instância do autor.
* Obter o driver de banco de dados JDBC (arquivo JAR) do provedor de banco de dados. Os exemplos no tutorial são baseados em [!DNL MySQL] banco de dados e uso [!DNL Oracle's] [Driver de banco de dados JDBC MySQL](https://dev.mysql.com/downloads/connector/j/5.1.html).

* Configure um banco de dados contendo dados do cliente com os campos exibidos abaixo. Um banco de dados não é essencial para criar um formulário adaptável. Este tutorial usa um banco de dados para exibir o modelo de dados de formulário e os recursos de persistência do AEM [!DNL Forms].

![adaptiveformdata](assets/adaptiveformdata.png)

## Etapa 1: Criar um formulário adaptável {#step-create-an-adaptive-form}

![03-criar-formulário-adaptável-imagem-principal_pequeno](assets/03-create-adaptive-form-main-image_small.png)

Os formulários adaptáveis são de nova geração, envolventes, responsivos, dinâmicos e de natureza adaptável. Usando formulários adaptáveis, você pode fornecer experiências personalizadas e direcionadas. AEM [!DNL Forms] forneça um editor WYSIWYG de arrastar e soltar para criar formulários adaptáveis. Para obter mais informações sobre formulários adaptáveis, consulte [Introdução à criação de formulários adaptáveis](../../forms/using/introduction-forms-authoring.md).

Metas:

* Criar um formulário adaptável que permita ao cliente adicionar um endereço de entrega
* Campos de layout de um formulário adaptável para exibir e aceitar informações de um cliente
* Criar ação de envio para enviar um email com conteúdo de formulário
* Pré-visualizar e enviar um formulário adaptável

[![Consulte o guia](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## Etapa 2: Criar modelo de dados do formulário {#step-create-form-data-model}

![05-criar-formulário-modelo-dados-principal_pequeno](assets/05-create-form-data-model-main_small.png)

Um modelo de dados de formulário permite conectar um formulário adaptável a fontes de dados diferentes. Por exemplo, perfil de usuário AEM, serviços Web RESTful, serviços Web baseados em SOAP, serviços OData e bancos de dados relacionais. Um modelo de dados de formulário é um esquema de representação de dados unificada de entidades e serviços comerciais disponíveis em fontes de dados conectadas. Você pode usar o modelo de dados de formulário com um formulário adaptável para recuperar, atualizar, excluir e adicionar dados às fontes de dados conectadas.

Metas:

* Configurar a instância do banco de dados do site ([!DNL MySQL] banco de dados) como fontes de dados
* Crie o modelo de dados de formulário usando [!DNL MySQL] banco de dados como fonte de dados
* Adicionar objetos de modelo de dados ao modelo de dados de formulário
* Configurar serviços de leitura e gravação para o modelo de dados de formulário
* Testar o modelo de dados do formulário e os serviços configurados com dados de teste

[![Consulte o guia](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## Etapa 3: Aplicar regras a campos de formulário adaptáveis {#step-apply-rules-to-adaptive-form-fields}

![07-aplicar-regras-ao-formulário-adaptável_pequeno](assets/07-apply-rules-to-adaptive-form_small.png)

Os formulários adaptáveis fornecem um editor para gravar regras em objetos de formulário adaptáveis. Essas regras definem as ações a serem acionadas nos objetos de formulário com base nas condições predefinidas, entradas do usuário e ações do usuário no formulário. Ele ajuda a garantir a precisão e acelera a experiência de preenchimento de formulários.

Metas:

* Criar e aplicar regras a campos de formulário adaptáveis
* Usar regras para acionar serviços de modelo de dados de formulário para atualizar dados para o banco de dados

[![Consulte o guia](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## Etapa 4: Crie o estilo do formulário adaptável {#step-style-your-adaptive-form}

![estilo de formulário adaptável](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

Os formulários adaptáveis fornecem temas e uma [editor](../../forms/using/themes.md) para criar temas para os formulários adaptáveis. Um tema contém detalhes de estilo para componentes e painéis, e você pode reutilizar um tema em diferentes formas. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência, alinhamento e tamanho. Quando você aplica o tema ao formulário, o estilo especificado é refletido nos componentes correspondentes do formulário. Os formulários adaptáveis também aceitam estilos em linha para estilos específicos de um formulário.

Metas:

* Aplicar um tema pronto para uso a um formulário adaptável
* Criar um tema para formulário adaptável usando o editor de temas
* Usar fontes da Web em um tema personalizado

[![Consulte o guia](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## Etapa 5: publique seu formulário adaptável {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-small](assets/12-publish-your-adaptive-form-_small.png)

É possível publicar formulários adaptáveis como um formulário independente (aplicativo de página única), incluindo no AEM [Página Sites](/help/forms/using/embed-adaptive-form-aem-sites.md), ou listar em um AEM [!DNL Site] usar [Portal Forms](../../forms/using/introduction-publishing-forms.md).

Metas:

* Publicar o formulário adaptável como uma página AEM
* Incorporar o formulário adaptável em um AEM [!DNL Sites] Página
* Incorpore o formulário adaptável em uma página externa da Web (uma página da Web não AEM hospedada fora do AEM)

[![Consulte o guia](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)
