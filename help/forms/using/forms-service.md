---
title: Serviço do Forms
seo-title: Serviço do Forms
description: O artigo descreve o serviço Forms e as tarefas relacionadas a formulários que você pode executar usando o serviço Forms.
seo-description: O artigo descreve o serviço Forms e as tarefas relacionadas a formulários que você pode executar usando o serviço Forms.
uuid: 3258d3c2-8755-4815-8c97-b2cfb9a9dfd4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: a9695d10-43ec-40eb-942f-7720abaa0973
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 6%

---


# Serviço do Forms {#forms-service}

## Visão geral {#overview}

O serviço Forms permite que você crie aplicativos clientes de captura de dados interativos que validam, processam, transformam e entregam formulários normalmente criados no Designer. O serviço Forms renderiza como documentos PDF qualquer design de formulário desenvolvido.

O serviço Forms também permite que as organizações estendam seus processos de captura de dados inteligente ao implantar formulários eletrônicos como PDFs Adobe. Você também pode usar o serviço para importar e exportar dados de e para PDF forms existentes, respectivamente.

Use o serviço Forms para fazer o seguinte:

* Renderize PDF forms com base em modelo e dados XML.
* Permitir que a integração de dados de formulário importe dados para e extraia dados de PDF forms.
* Renderize formulários com base em fragmentos.

## Criação de PDF forms  {#creating-pdf-forms-nbsp}

Use o serviço de Formulário para criar PDF forms para captura de dados. Geralmente, você start um modelo do AEM Forms Designer. Use a operação `renderPDFForm` (link para Javadoc) do serviço Forms para converter esse modelo em um formulário PDF.

O primeiro parâmetro da operação `renderPDFForm` é o nome do arquivo de modelo (por exemplo, `ExpenseClaim.xdp`). Você pode armazenar o arquivo de modelo em um sistema de arquivos local, repositório CRX ou em um local HTTP ou FTP. Você pode especificar o local do arquivo de modelo definindo a raiz do conteúdo no parâmetro `PDFFormRenderOptions` da operação `renderPDFForm`. Consulte Javadoc para obter detalhes de outras opções que você pode especificar para o parâmetro `PDFFormRenderOptions`.

A operação `renderPDFForm` também pode aceitar dados XML. Os dados XML são unidos ao modelo ao criar um formulário PDF para que o formulário PDF gerado contenha os dados especificados. O segundo parâmetro para a operação `renderPDFForm` pode aceitar um objeto de Documento (Javadoc) que contenha dados XML.

## Extrair dados de PDF forms  {#extracting-data-from-pdf-forms-nbsp}

Use a operação `exportData` (Javadoc) do serviço Forms para extrair dados XML de um formulário PDF. Esta operação aceita um documento como seu primeiro parâmetro. É possível exportar os dados como um documento XDP ou um arquivo XML. Se você exportar os dados como um arquivo XML, os dados exportados removerão o envelope XDP e retornarão um arquivo XML simples. Você pode especificar essa disposição usando o segundo parâmetro.

## Importação de dados para PDF forms {#importing-data-into-pdf-forms}

O serviço Forms também permite unir um formulário PDF criado usando o AEM Forms Designer ou a operação `renderPDFForm` com dados XML. A operação `importData` (Javadoc) do serviço Forms aceita o formulário PDF e os dados XML e retorna um formulário PDF com XML de dados.

## Renderização de formulários com base em fragmentos {#rendering-forms-based-on-fragments}

O serviço Forms pode renderizar formulários com base em fragmentos criados por você usando o AEM Forms Designer. Um fragmento é uma parte reutilizável de um formulário. Ele é salvo como um arquivo XDP separado que pode ser inserido em vários designs de formulário. Por exemplo, um fragmento pode incluir um bloco de endereço ou texto legal.

O uso de fragmentos simplifica e acelera a criação e a manutenção de um grande número de formulários. Ao criar um formulário, insira uma referência ao fragmento necessário para que o fragmento apareça no formulário. A referência do fragmento contém um subformulário que aponta para o arquivo XDP físico.

Estas são as vantagens do uso de fragmentos:

* **Reutilização** de conteúdo: É possível reutilizar o conteúdo em vários designs de formulário. Para reutilizar rapidamente partes do mesmo conteúdo em vários formulários, crie um fragmento. A cópia ou recriação do conteúdo leva mais tempo. O uso de fragmentos também garante que as partes de um design de formulário usadas frequentemente possuam conteúdo e aparência consistentes em todos os formulários de referência.
* **Atualizações** globais: É possível fazer alterações globais em vários formulários apenas uma vez em um arquivo. É possível alterar o conteúdo, objetos de script, vínculos de dados, layout ou estilos em um fragmento. Todos os formulários XDP que fazem referência ao fragmento refletem as alterações.
* **Criação** de formulários compartilhados: É possível compartilhar a criação de formulários entre vários recursos. Os desenvolvedores de formulários com experiência em scripts ou outros recursos avançados do AEM Forms Designer podem desenvolver e compartilhar fragmentos que usam propriedades dinâmicas e de scripts. Os designers de formulário podem usar os fragmentos para criar formulários. Além disso, eles podem usar os fragmentos para garantir que todas as partes de um formulário tenham uma aparência e funcionalidade consistentes em vários formulários.

