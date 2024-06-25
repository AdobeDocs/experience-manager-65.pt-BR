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
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Serviço do Forms {#forms-service}

## Visão geral {#overview}

O serviço Forms permite criar aplicativos cliente de captura de dados interativos que validam, processam, transformam e fornecem formulários que normalmente são criados no Designer. O serviço Forms renderiza como PDF qualquer design de formulário desenvolvido por você.

O serviço Forms também permite que as organizações estendam seus processos inteligentes de captura de dados, implantando formulários eletrônicos como PDF Adobe. Você também pode usar o serviço para importar e exportar dados de e para PDF forms existentes, respectivamente.

Use o serviço Forms para fazer o seguinte:

* Renderiza PDF forms com base no modelo e nos dados XML.
* Habilite a integração de dados de formulário para importar e extrair dados do PDF forms.
* Renderizar formulários com base em fragmentos.

## Criar PDF forms  {#creating-pdf-forms-nbsp}

Use o Serviço de formulário para criar PDF forms para captura de dados. Normalmente, você começa com um modelo do AEM Forms Designer. Use o `renderPDFForm` (link para Javadoc) operação do serviço Forms para converter esse template em um formulário PDF.

O primeiro parâmetro da variável `renderPDFForm` operation é o nome do arquivo de modelo (por exemplo, `ExpenseClaim.xdp`). Você pode armazenar o arquivo de modelo em um sistema de arquivos local, repositório CRX ou em um local HTTP ou FTP. Você pode especificar o local do arquivo de modelo definindo a raiz do conteúdo no `PDFFormRenderOptions` parâmetro do `renderPDFForm` operação. Consulte Javadoc para obter detalhes de outras opções que podem ser especificadas para o `PDFFormRenderOptions` parâmetro.

A variável `renderPDFForm` A operação do também pode aceitar dados XML. Os dados XML são mesclados com o modelo ao criar um Formulário de PDF para que o formulário de PDF gerado contenha os dados especificados. O segundo parâmetro para a variável `renderPDFForm` A operação pode aceitar um objeto Documento (Javadoc) que contém dados XML.

## Extração de dados do PDF forms  {#extracting-data-from-pdf-forms-nbsp}

Use o `exportData` (Javadoc) operação do serviço Forms para extrair dados XML de um formulário PDF. Esta operação aceita um documento como seu primeiro parâmetro. Você pode exportar os dados como um documento XDP ou um arquivo XML. Se exportar os dados como um arquivo XML, os dados exportados removerão o envelope XDP e retornarão um arquivo XML simples. Você pode especificar essa organização usando o segundo parâmetro.

## Importação de dados para o PDF forms {#importing-data-into-pdf-forms}

O serviço Forms também permite mesclar um formulário PDF criado com o AEM Forms Designer ou com o `renderPDFForm` operação com dados XML. A variável `importData` (Javadoc) operação do serviço Forms aceita o formulário PDF e os dados XML e retorna um formulário PDF com dados XML.

## Renderização de formulários com base em fragmentos {#rendering-forms-based-on-fragments}

O serviço do Forms pode renderizar formulários com base em fragmentos criados usando o AEM Forms Designer. Um fragmento é uma parte reutilizável de um formulário. Ele é salvo como um arquivo XDP separado que pode ser inserido em vários designs de formulário. Por exemplo, um fragmento pode incluir um bloco de endereço ou texto legal.

O uso de fragmentos simplifica e acelera a criação e a manutenção de um grande número de formulários. Ao criar um formulário, insira uma referência ao fragmento necessário para que o fragmento apareça no formulário. A referência do fragmento contém um subformulário que aponta para o arquivo XDP físico.

Estas são as vantagens de usar fragmentos:

* **Reutilização de conteúdo**: é possível reutilizar o conteúdo em vários designs de formulário. Para reutilizar rapidamente partes do mesmo conteúdo em vários formulários, crie um fragmento. Copiar ou recriar o conteúdo leva mais tempo. O uso de fragmentos também garante que as partes usadas com frequência de um design de formulário tenham conteúdo e aparência consistentes em todos os formulários de referência.
* **Atualizações globais**: é possível fazer alterações globais em vários formulários apenas uma vez em um arquivo. Você pode alterar o conteúdo, os objetos de script, as associações de dados, o layout ou os estilos em um fragmento. Todos os formulários XDP que fazem referência ao fragmento refletem as alterações.
* **Criação de formulário compartilhado**: é possível compartilhar a criação de formulários entre vários recursos. Desenvolvedores de formulários com experiência em script ou outros recursos avançados do AEM Forms Designer podem desenvolver e compartilhar fragmentos que usam script e propriedades dinâmicas. Os designers de formulários podem usar os fragmentos para criar formulários. Além disso, eles podem usar os fragmentos para garantir que todas as partes de um formulário tenham uma aparência e funcionalidade consistentes em vários formulários.
