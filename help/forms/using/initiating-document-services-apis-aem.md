---
title: Iniciar APIs de Serviços de documento a partir do fluxo de trabalho do AEM
seo-title: Initiate Document Services APIs from AEM Workflow
description: Saiba como invocar serviços de documento AEM no DDX ou nas entradas fornecidas. Veja também como converter PDF em PDF/A
seo-description: Learn how to invoke AEM Document services on DDX or supplied inputs. Also see hwo to convert PDF to PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
exl-id: 123087a2-9d09-4579-9185-2ccd7d25bf8d
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# Iniciar APIs de Serviços de documento a partir do fluxo de trabalho do AEM  {#initiate-document-services-apis-from-aem-workflow}

## Assembler {#assembler}

O AEM Forms fornece fluxos de trabalho personalizados para chamar as seguintes APIs de serviço do Assembler:

* **invocar**: invoca operações especificadas no DDX de entrada nas entradas fornecidas.
* **toPDFA**: converte o documento de PDF de entrada em um documento PDF/A.

### Chamar fluxo de trabalho DDX {#invoke-ddx-workflow}

A variável **Chamar DDX** o fluxo de trabalho chama a variável `Invoke` API de serviço do Assembler, que pode ser usada para montar ou desmontar documentos, adicionar marca d&#39;água a um PDF e assim por diante.

1. Arraste o **[!UICONTROL Chamar DDX]** etapa do fluxo de trabalho na guia Forms Workflow no Sidekick.
1. Clique duas vezes na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, opções de ambiente e documentos de saída e clique em **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents}

O fluxo de trabalho Chamar DDX requer os seguintes documentos de entrada:

* **DDX**: é uma entrada obrigatória para a etapa Chamar fluxo de trabalho DDX e pode ser especificada selecionando uma das seguintes opções no menu suspenso Entrada DDX.

   * *Relativo À Carga Útil*: o arquivo de entrada DDX é relativo à pasta da carga útil do item do fluxo de trabalho.
   * *Usar carga útil*: a carga do item do fluxo de trabalho é usada como o documento DDX de entrada.
   * *Caminho absoluto*: o caminho absoluto para o documento DDX no repositório CRX.

* **Criar Mapa a partir do PayLoad**: quando selecionado, todos os documentos na pasta de carga útil são adicionados ao Mapa do documento de entrada para o `invoke` API no Assembler. O nome do nó de cada documento é usado como uma chave no mapa.

* **Mapa do documento de entrada**: especifica o mapa do documento de entrada. Você pode adicionar qualquer número de entradas, onde cada entrada especifica a chave do documento no mapa e a origem do documento.

#### Opções de ambiente {#environment-options}

A guia Opções de ambiente permite definir várias opções de processamento para a API invoke.

* *Nível de registro da tarefa*: especifica o nível de log para os logs de processamento.
* *Validar apenas*: verifica a validade do DDX de entrada.

* *Falha ao errar*: especifica se a chamada para o serviço Assembler deve falhar se houver um erro. O valor padrão é Falso.

#### Documentos de saída {#output-documents}

Dependendo do DDX de entrada, a API invoke pode produzir vários documentos de saída. A guia Documentos de saída permite selecionar onde o documento de saída será salvo.

1. *Salvar saída na carga útil*: salva os documentos de saída na pasta de carga útil, ou substitui a carga útil, se a carga útil for um arquivo.
1. *Mapa do documento de saída*: permite especificar explicitamente onde salvar cada documento de saída, adicionando uma entrada por documento de saída. Cada entrada especifica o documento e onde salvá-lo. Um documento de saída pode substituir o conteúdo ou ser salvo na pasta de conteúdo. É útil quando há vários documentos de saída.

1. *Registro da tarefa*: especifica onde salvar o documento de log do trabalho, o que é útil para solucionar falhas.

### Converter em fluxo de trabalho do PDF/A {#convert-to-pdf-a-workflow}

A etapa de fluxo de trabalho Converter em PDF/A chama a variável `toPDFA` API de serviço do Assembler. Ele é usado para converter documentos PDF em documentos compatíveis com PDF/A.

1. Arraste o **[!UICONTROL ConvertToPDFA]** etapa do fluxo de trabalho na guia Forms Workflow no Sidekick.

1. Clique duas vezes na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, opções de conversão e documentos de saída e clique em **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents-1}

Especifique a origem do documento a ser convertido em um documento compatível com PDF/A de uma das seguintes maneiras.

* *Relativo À Carga Útil*: o documento de entrada é relativo à pasta de carga útil do item do fluxo de trabalho.
* *Usar carga útil*: a carga do item do workflow é usada como o documento de entrada.
* *Caminho absoluto*: o caminho absoluto do documento de entrada no repositório CRX.

#### Opções de conversão {#conversion-options}

As Opções de conversão permitem especificar opções que alteram o processo de conversão de PDF/A.

* *Conformidade* : especifica o padrão PDF/A que o PDF/A de saída deve atender.
* *Nível do resultado* : especifica o nível de log a ser usado para logs de conversão de PDF/A.
* *Assinaturas* : especifica como as assinaturas no documento de entrada devem ser processadas durante a conversão.
* *Espaço de cor* : especifica o espaço de cores predefinido a ser usado para o documento PDF/A de saída.
* *Verificar* Conversão: especifica se o documento de PDF/A convertido deve ser verificado quanto à conformidade de PDF/A após a conversão.
* *Nível de registro da tarefa* : especifica o nível de log a ser usado para processar logs.

* *Esquema de extensão de metadados* : especifica o caminho para o esquema de extensão de metadados a ser usado para propriedades XMP nos metadados do documento PDF.

#### Documentos de saída {#output-documents-1}

A guia Documentos de saída permite especificar o destino dos documentos de saída

* *Documento PDFA*: especifica o local onde o documento PDF/A convertido é salvo. Ele pode substituir o documento de carga útil ou ser salvo na pasta de carga útil.
* *Log de conversão*: especifica o local onde os logs de conversão são salvos. Ele pode substituir o documento de carga útil ou ser salvo na pasta de carga útil.

## Forms {#forms}

O fluxo de trabalho Renderizar formulário PDF é um invólucro ao redor `renderPDFForm` API de serviço do Forms para criar um formulário PDF usando um modelo XDP e xml de dados.

### Renderizar fluxo de trabalho do Formulário de PDF {#render-pdf-form-workflow}

1. Arraste a etapa Renderizar fluxo de trabalho de PDF para a guia Forms Workflow no Sidekick.
1. Clique duas vezes na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, documentos de saída e parâmetros adicionais e clique em **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents-2}

* *Arquivo modelo*: especifica o local do modelo XDP. É um campo obrigatório.

* *Documento de dados*: especifica o local do xml de dados que precisa ser mesclado com o modelo.

#### Documentos de saída {#output-documents-2}

* *Documento de saída*: - Especifica o nome do formulário de PDF gerado.

#### Parâmetros adicionais {#additional-parameters}

* *Raiz de conteúdo*: especifica o caminho para a pasta no repositório onde os fragmentos ou imagens usados no modelo XDP de entrada são armazenados.
* *Enviar URL*: especifica o URL de envio padrão para o formulário de PDF gerado.
* *Localidade*: especifica a localidade padrão para o formulário de PDF gerado.
* *Versão do Acrobat*: especifica a versão de destino do Acrobat para o formulário de PDF gerado.
* *PDF marcado*: especifica se o PDF gerado deve ficar acessível.
* *Documento XCI*: especifica o caminho para o arquivo XCI.

## Saída {#output}

O fluxo de trabalho Gerar PDF não interativo é um invólucro `generatePDFOutput` API do serviço de saída. Ele é usado para gerar documentos de PDF não interativos do modelo XDP e do xml de dados.

### Gerar fluxo de trabalho de saída de PDF não interativo   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. Arraste o workflow Gerar saída de PDF não interativa para a guia Forms Workflow no Sidekick.
1. Clique duas vezes na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, documentos de saída e parâmetros adicionais e clique em **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents-3}

* *Arquivo modelo*: especifica o local do modelo XDP. É um campo obrigatório.

* *Documento de dados*: especifica o local do xml de dados que precisa ser mesclado com o modelo.

#### Documento de saída {#output-document}

*Documento de saída*: especifica o nome do formulário de PDF gerado.

#### Parâmetros adicionais {#additional-parameters-1}

* *Raiz de conteúdo*: especifica o caminho para a pasta no repositório onde os fragmentos ou imagens usados no modelo XDP de entrada são armazenados.
* *Localidade*: especifica a localidade padrão para o formulário de PDF gerado.
* *Versão do Acrobat*: especifica a versão de destino do Acrobat para o formulário de PDF gerado.
* PDF linearizado: especifica se o PDF gerado deve ser otimizado para visualização na Web.
* *PDF marcado*: especifica se o PDF gerado deve ficar acessível.
* *Documento XCI*: especifica o caminho para o arquivo XCI.
