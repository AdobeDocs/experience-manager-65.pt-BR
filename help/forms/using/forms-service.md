---
title: Serviço do Forms
description: O artigo descreve o serviço Forms e as tarefas relacionadas ao formulário que podem ser executadas usando o serviço Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services,Forms Service,PDF Generator
exl-id: 6580fe6f-3cdb-45ec-8ba3-51dc60d1965e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: b59c0486-3350-52ed-8816-e0a8e11486b8
    internal-label: Forms Service
  - id: b26425d0-6fde-5e02-bfd6-e560e2fa86c9
    internal-label: PDF Generator
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%
---
# Serviço do Forms {#forms-service}

## Visão geral {#overview}

O serviço Forms permite criar aplicativos cliente de captura de dados interativos que validam, processam, transformam e fornecem formulários que normalmente são criados no Designer. O serviço Forms renderiza como documentos do PDF qualquer design de formulário que você desenvolve.

O serviço Forms também permite que as organizações estendam seus processos inteligentes de captura de dados implantando formulários eletrônicos como PDFs Adobe. Você também pode usar o serviço para importar e exportar dados de e para o PDF forms existente, respectivamente.

Use o serviço Forms para fazer o seguinte:

* Renderize o PDF forms com base no modelo e nos dados XML.
* Habilite a integração de dados de formulário para importar e extrair dados do PDF forms.
* Renderizar formulários com base em fragmentos.

## Criação do PDF forms  {#creating-pdf-forms-nbsp}

Use o serviço de formulário para criar PDF forms para captura de dados. Normalmente, você começa com um modelo do AEM Forms Designer. Use a operação `renderPDFForm` (link para Javadoc) do serviço Forms para converter este modelo em um formulário do PDF.

O primeiro parâmetro da operação `renderPDFForm` é o nome do arquivo de modelo (por exemplo, `ExpenseClaim.xdp`). Você pode armazenar o arquivo de modelo em um sistema de arquivos local, repositório do CRX ou em um local HTTP ou FTP. Você pode especificar o local do arquivo de modelo definindo a raiz do conteúdo no parâmetro `PDFFormRenderOptions` da operação `renderPDFForm`. Consulte Javadoc para obter detalhes de outras opções que você pode especificar para o parâmetro `PDFFormRenderOptions`.

A operação `renderPDFForm` também pode aceitar dados XML. Os dados XML são mesclados com o modelo ao criar um formulário do PDF para que o formulário do PDF gerado contenha os dados especificados. O segundo parâmetro da operação `renderPDFForm` pode aceitar um objeto Document (Javadoc) que contenha dados XML.

## Extração de dados do PDF forms  {#extracting-data-from-pdf-forms-nbsp}

Use a operação `exportData` (Javadoc) do serviço Forms para extrair dados XML de um formulário PDF. Esta operação aceita um documento como seu primeiro parâmetro. Você pode exportar os dados como um documento XDP ou um arquivo XML. Se exportar os dados como um arquivo XML, os dados exportados removerão o envelope XDP e retornarão um arquivo XML simples. Você pode especificar essa organização usando o segundo parâmetro.

## Importação de dados para o PDF forms {#importing-data-into-pdf-forms}

O serviço Forms também permite mesclar um formulário do PDF criado com o AEM Forms Designer ou a operação `renderPDFForm` com dados XML. A operação `importData` (Javadoc) do serviço Forms aceita o formulário PDF e os dados XML e retorna um formulário PDF com dados XML.

## Renderização de formulários com base em fragmentos {#rendering-forms-based-on-fragments}

O serviço do Forms pode renderizar formulários com base em fragmentos criados usando o AEM Forms Designer. Um fragmento é uma parte reutilizável de um formulário. Ele é salvo como um arquivo XDP separado que pode ser inserido em vários designs de formulário. Por exemplo, um fragmento pode incluir um bloco de endereço ou texto legal.

O uso de fragmentos simplifica e acelera a criação e a manutenção de um grande número de formulários. Ao criar um formulário, insira uma referência ao fragmento necessário para que o fragmento apareça no formulário. A referência do fragmento contém um subformulário que aponta para o arquivo XDP físico.

Estas são as vantagens de usar fragmentos:

* **Reutilização de conteúdo**: é possível reutilizar conteúdo em vários designs de formulário. Para reutilizar rapidamente partes do mesmo conteúdo em vários formulários, crie um fragmento. Copiar ou recriar o conteúdo leva mais tempo. O uso de fragmentos também garante que as partes usadas com frequência de um design de formulário tenham conteúdo e aparência consistentes em todos os formulários de referência.
* **Atualizações globais**: você pode fazer alterações globais em vários formulários apenas uma vez em um arquivo. Você pode alterar o conteúdo, os objetos de script, as associações de dados, o layout ou os estilos em um fragmento. Todos os formulários XDP que fazem referência ao fragmento refletem as alterações.
* **Criação de formulário compartilhado**: você pode compartilhar a criação de formulários entre vários recursos. Desenvolvedores de formulários com experiência em script ou outros recursos avançados do AEM Forms Designer podem desenvolver e compartilhar fragmentos que usam script e propriedades dinâmicas. Os designers de formulários podem usar os fragmentos para criar formulários. Além disso, eles podem usar os fragmentos para garantir que todas as partes de um formulário tenham uma aparência e funcionalidade consistentes em vários formulários.
