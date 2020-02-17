---
title: Iniciar APIs do Document Services a partir do fluxo de trabalho do AEM
seo-title: Iniciar APIs do Document Services a partir do fluxo de trabalho do AEM
description: Saiba como chamar os serviços de documento AEM no DDX ou em entradas fornecidas. Veja também como converter PDF em PDF/A
seo-description: Saiba como chamar os serviços de documento AEM no DDX ou em entradas fornecidas. Veja também como converter PDF em PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
translation-type: tm+mt
source-git-commit: 7caf09f7020c066072eac04a349a19b144dfeb7b

---


# Iniciar APIs do Document Services a partir do fluxo de trabalho do AEM {#initiate-document-services-apis-from-aem-workflow}

## Assembler {#assembler}

O AEM Forms fornece fluxos de trabalho personalizados para chamar as seguintes APIs de serviço do Assembler:

* **invocar**: Chama as operações especificadas no DDX de entrada nas entradas fornecidas.
* **toPDFA**: Converte o documento PDF de entrada em documento PDF/A.

### Chamar fluxo de trabalho DDX {#invoke-ddx-workflow}

O fluxo de trabalho **Invocar DDX** chama a API de serviço do `Invoke` Assembler, que você pode usar para montar ou desmontar documentos, adicionar uma marca d&#39;água a um PDF e assim por diante.

1. Arraste a etapa de fluxo de trabalho **[!UICONTROL Invocar DDX]** na guia Fluxo de trabalho de formulários no Sidekick.
1. Clique duas vezes na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, opções de ambiente e documentos de saída e clique em **[!UICONTROL OK]**.

#### Input documents {#input-documents}

O fluxo de trabalho Invocar DDX requer os seguintes documentos de entrada:

* **DDX**: É uma entrada obrigatória para a etapa de fluxo de trabalho Invocar DDX e pode ser especificada selecionando uma das seguintes opções no menu suspenso de entrada DDX.

   * *Em Relação À Carga*: O arquivo de entrada DDX é relativo à pasta de carga do item de fluxo de trabalho.
   * *Usar carga*: A carga do item de fluxo de trabalho é usada como o documento DDX de entrada.
   * *Caminho* absoluto: O caminho absoluto para o documento DDX no repositório CRX.

* **Criar mapa do PayLoad**: Quando selecionados, todos os documentos na pasta de carga são adicionados ao Mapa do documento de entrada para a `invoke` API no Assembler. O nome do nó de cada documento é usado como uma chave no mapa.

* **Mapa** do documento de entrada: Especifica o mapa do documento de entrada. É possível adicionar qualquer número de entradas, em que cada entrada especifica a chave do documento no mapa e a origem do documento.

#### Environment options {#environment-options}

A guia Opções de ambiente permite definir várias opções de processamento para a API de chamada.

* *Nível* do log de tarefas: Especifica o nível de log dos logs de processamento.
* *Validar somente*: Verifica a validade do DDX de entrada.

* *Erro* de falha: Especifica se a chamada para o serviço Assembler deve falhar em caso de erro. O valor padrão é Falso.

#### Output documents {#output-documents}

Dependendo do DDX de entrada, a API de chamada pode produzir vários documentos de saída. A guia Documentos de saída permite selecionar onde o documento de saída será salvo.

1. *Salvar saída na carga*: Salva documentos de saída na pasta de carga ou substitui a carga, se a carga for um arquivo.
1. *Mapa* do documento de saída: Permite especificar explicitamente onde salvar cada documento de saída adicionando uma entrada por documento de saída. Cada entrada especifica o documento e onde salvá-lo. Um documento de saída pode substituir a carga ou pode ser salvo na pasta da carga. É útil quando há vários documentos de saída.

1. *Log* de tarefas: Especifica onde salvar o documento de log de trabalhos, que é útil para solucionar problemas de falhas.

### Convert to PDF/A workflow {#convert-to-pdf-a-workflow}

A etapa de fluxo de trabalho Converter em PDF/A chama a API de serviço do `toPDFA` Assembler. É usado para converter documentos PDF em documentos compatíveis com PDF/A.

1. Arraste a etapa de fluxo de trabalho **[!UICONTROL ConvertToPDFA]** na guia Fluxo de trabalho de formulários no Sidekick.

1. Clique duas vezes na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, opções de conversão e documentos de saída e clique em **[!UICONTROL OK]**.

#### Input documents {#input-documents-1}

Especifique a origem do documento a ser convertido em um documento compatível com PDF/A de uma das seguintes maneiras.

* *Em Relação À Carga*: O documento de entrada é relativo à pasta de carga do item de fluxo de trabalho.
* *Usar carga*: A carga do item de fluxo de trabalho é usada como o documento de entrada.
* *Caminho* absoluto: O caminho absoluto do documento de entrada no repositório CRX.

#### Conversion options {#conversion-options}

As Opções de conversão permitem especificar opções que alteram o processo de conversão de PDF/A.

* *Conformidade* : Especifica o padrão PDF/A ao qual o PDF/A de saída deve estar em conformidade.
* *Nível* de resultado: Especifica o nível de log a ser usado para logs de conversão de PDF/A.
* *Assinaturas* : Especifica como as assinaturas no documento de entrada devem ser processadas durante a conversão.
* *Espaço* colorido: Especifica o espaço de cor predefinido a ser usado para o documento PDF/A de saída.
* *Verificar* conversão: Especifica se o documento PDF/A convertido deve ser verificado para conformidade com PDF/A após a conversão.
* *Nível* do log de trabalhos: Especifica o nível de log a ser usado para os logs de processamento.

* *Esquema* de extensão de metadados: Especifica o caminho para o esquema de extensão de metadados a ser usado para propriedades XMP nos metadados do documento PDF.

#### Output documents {#output-documents-1}

A guia Documentos de saída permite especificar o destino dos documentos de saída

* *Documento* do PDFA: Especifica o local onde o documento PDF/A convertido é salvo. Ele pode substituir o documento de carga ou ser salvo na pasta de carga.
* *Log* de conversão: Especifica o local onde os logs de conversão são salvos. Ele pode substituir o documento de carga ou pode ser salvo na pasta de carga.

## Forms {#forms}

O fluxo de trabalho Renderizar formulário PDF é um invólucro da API de serviço do `renderPDFForm` Forms para criar um formulário PDF usando um modelo XDP e um xml de dados.

### Renderizar fluxo de trabalho do formulário PDF {#render-pdf-form-workflow}

1. Arraste a etapa de fluxo de trabalho Renderizar formulário PDF na guia Fluxo de trabalho de formulários no Sidekick.
1. Clique duas vezes na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, documentos de saída e parâmetros adicionais e clique em **[!UICONTROL OK]**.

#### Input documents {#input-documents-2}

* *Arquivo* de modelo: Especifica o local do modelo XDP. É um campo obrigatório.

* *Documento* de dados: Especifica o local do xml de dados que precisa ser unido ao modelo.

#### Output documents {#output-documents-2}

* *Documento* de saída: - Especifica o nome do formulário PDF gerado.

#### Parâmetros adicionais {#additional-parameters}

* *Raiz* do conteúdo: Especifica o caminho para a pasta no repositório onde os fragmentos ou imagens usados no modelo XDP de entrada são armazenados.
* *Enviar URL*: Especifica o URL de envio padrão para o formulário PDF gerado.
* *Local*: Especifica a localidade padrão para o formulário PDF gerado.
* *Versão* do Acrobat: Especifica a versão direcionada do Acrobat para o formulário PDF gerado.
* *PDF* marcado: Especifica se o PDF gerado deve ser acessível.
* *Documento* XCI: Especifica o caminho para o arquivo XCI.

## Saída {#output}

O Fluxo de trabalho Gerar PDF não interativo é um invólucro da API de serviço de `generatePDFOutput` Saída. É usado para gerar documentos PDF não interativos do modelo XDP e do xml de dados.

### Gerar fluxo de trabalho de saída de PDF não interativo {#generate-non-interactive-pdf-output-workflow-nbsp}

1. Arraste o fluxo de trabalho Gerar saída de PDF não interativa na guia Fluxo de trabalho de formulários no Sidekick.
1. Clique duas vezes na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, documentos de saída e parâmetros adicionais e clique em **[!UICONTROL OK]**.

#### Input documents {#input-documents-3}

* *Arquivo* de modelo: Especifica o local do modelo XDP. É um campo obrigatório.

* *Documento* de dados: Especifica o local do xml de dados que precisa ser unido ao modelo.

#### Output document {#output-document}

*Documento* de saída: Especifica o nome do formulário PDF gerado.

#### Parâmetros adicionais {#additional-parameters-1}

* *Raiz* do conteúdo: Especifica o caminho para a pasta no repositório onde os fragmentos ou imagens usados no modelo XDP de entrada são armazenados.
* *Local*: Especifica a localidade padrão para o formulário PDF gerado.
* *Versão* do Acrobat: Especifica a versão direcionada do Acrobat para o formulário PDF gerado.
* PDF linearizado: Especifica se o PDF gerado deve ser otimizado para visualização na Web.
* *PDF* marcado: Especifica se o PDF gerado deve ser acessível.
* *Documento* XCI: Especifica o caminho para o arquivo XCI.

