---
title: Iniciar APIs de serviços de Documento AEM fluxo de trabalho
seo-title: Iniciar APIs de serviços de Documento AEM fluxo de trabalho
description: Saiba como chamar AEM serviços de Documento no DDX ou em entradas fornecidas. Veja também como converter PDF em PDF/A
seo-description: Saiba como chamar AEM serviços de Documento no DDX ou em entradas fornecidas. Veja também como converter PDF em PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
translation-type: tm+mt
source-git-commit: 7caf09f7020c066072eac04a349a19b144dfeb7b
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---


# Iniciar APIs de serviços de Documento AEM fluxo de trabalho {#initiate-document-services-apis-from-aem-workflow}

## Assembler {#assembler}

A AEM Forms fornece workflows personalizados para chamar as seguintes APIs de serviço do Assembler:

* **invocar**: Chama as operações especificadas no DDX de entrada nas entradas fornecidas.
* **toPDFA**: Converte documento PDF de entrada em documento PDF/A.

### Chamar fluxo de trabalho DDX {#invoke-ddx-workflow}

O fluxo de trabalho **Invocar DDX** chama a `Invoke` API de serviço do Assembler, que você pode usar para montar ou desmontar documentos, adicionar uma marca d&#39;água a um PDF e assim por diante.

1. Arraste a etapa de fluxo de trabalho **[!UICONTROL Invocar DDX]** sob a guia Forms Workflow no Sidekick.
1. Clique com o duplo na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, opções de ambiente e documentos de saída e clique em **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents}

O fluxo de trabalho Invocar DDX requer os seguintes documentos de entrada:

* **DDX**: É uma entrada obrigatória para a etapa de fluxo de trabalho Invocar DDX e pode ser especificada selecionando uma das seguintes opções no menu suspenso de entrada DDX.

   * *Em Relação À Carga*: O arquivo de entrada DDX é relativo à pasta de carga do item de fluxo de trabalho.
   * *Usar carga*: A carga do item de fluxo de trabalho é usada como o documento DDX de entrada.
   * *Caminho* absoluto: O caminho absoluto para o documento DDX no repositório CRX.

* **Criar mapa do PayLoad**: Quando selecionados, todos os documentos na pasta payload são adicionados ao Mapa de Documentos de entrada para a  `invoke` API no Assembler. O nome do nó de cada documento é usado como uma chave no mapa.

* **Mapa** do Documento de entrada: Especifica o Mapa de Documentos de entrada. É possível adicionar qualquer número de entradas, onde cada entrada especifica a chave do documento no mapa e a fonte do documento.

#### Opções de ambiente {#environment-options}

A guia Opções de Ambiente permite definir várias opções de processamento para a API de chamada.

* *Nível* do log de tarefas: Especifica o nível de log dos logs de processamento.
* *Validar somente*: Verifica a validade do DDX de entrada.

* *Erro* de falha: Especifica se a chamada para o serviço Assembler deve falhar em caso de erro. O valor padrão é Falso.

#### Documentos de saída {#output-documents}

Dependendo do DDX de entrada, a API de chamada pode produzir vários documentos de saída. A guia Documentos de saída permite selecionar onde o documento de saída será salvo.

1. *Salvar saída na carga*: Salva documentos de saída na pasta de carga ou substitui a carga, se a carga for um arquivo.
1. *Mapa* do Documento de saída: Permite especificar explicitamente onde salvar cada documento de saída adicionando uma entrada por documento de saída. Cada entrada especifica o documento e onde salvá-lo. Um documento de saída pode substituir a carga ou pode ser salvo na pasta da carga. É útil quando há vários documentos de saída.

1. *Log* de tarefas: Especifica onde salvar o documento de log de trabalhos, que é útil para solucionar problemas de falhas.

### Converter em fluxo de trabalho PDF/A {#convert-to-pdf-a-workflow}

A etapa de fluxo de trabalho Converter em PDF/A chama a `toPDFA` API de serviço do Assembler. É usado para converter documentos PDF em documentos compatíveis com PDF/A.

1. Arraste a etapa de fluxo de trabalho **[!UICONTROL ConvertToPDFA]** para baixo da guia Forms Workflow no Sidekick.

1. Clique com o duplo na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, opções de conversão e documentos de saída e clique em **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents-1}

Especifique a fonte do documento para conversão em um documento compatível com PDF/A de uma das seguintes maneiras.

* *Em Relação À Carga*: O documento de entrada é relativo à pasta de carga do item de fluxo de trabalho.
* *Usar carga*: A carga do item de fluxo de trabalho é usada como o documento de entrada.
* *Caminho* absoluto: O caminho absoluto do documento de entrada no repositório CRX.

#### Opções de conversão {#conversion-options}

As Opções de conversão permitem especificar opções que alteram o processo de conversão de PDF/A.

* *Conformidade* : Especifica o padrão PDF/A ao qual o PDF/A de saída deve estar em conformidade.
* *Nível*  de resultado: Especifica o nível de log a ser usado para logs de conversão de PDF/A.
* *Assinaturas* : Especifica como as assinaturas no documento de entrada devem ser processadas durante a conversão.
* *Espaço*  de cor: Especifica o espaço de cor predefinido a ser usado para o documento PDF/A de saída.
* ** VerifyConversion: Especifica se o documento PDF/A convertido deve ser verificado para compatibilidade com PDF/A após a conversão.
* *Nível*  do log de tarefas: Especifica o nível de log a ser usado para os logs de processamento.

* *Schema de extensão*  de metadados: Especifica o caminho para o schema de extensão de metadados a ser usado para XMP propriedades nos metadados do documento PDF.

#### Documentos de saída {#output-documents-1}

A guia Documentos de saída permite especificar o destino dos documentos de saída

* *DOCUMENTO* PDFA: Especifica o local onde o documento PDF/A convertido é salvo. Ele pode substituir o documento da carga ou ser salvo na pasta da carga.
* *Log* de conversão: Especifica o local onde os logs de conversão são salvos. Ele pode substituir o documento de carga ou pode ser salvo na pasta de carga.

## Forms {#forms}

O fluxo de trabalho Renderizar formulário PDF é um invólucro da `renderPDFForm` API de serviço da Forms para criar um formulário PDF usando um modelo XDP e um xml de dados.

### Renderizar fluxo de trabalho do formulário PDF {#render-pdf-form-workflow}

1. Arraste a etapa de fluxo de trabalho Renderizar formulário PDF na guia Forms Workflow no Sidekick.
1. Clique com o duplo na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, documentos de saída e parâmetros adicionais e clique em **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents-2}

* *Arquivo* de modelo: Especifica o local do modelo XDP. É um campo obrigatório.

* *Documento* de dados: Especifica o local do xml de dados que precisa ser unido ao modelo.

#### Documentos de saída {#output-documents-2}

* *Documento* de saída: - Especifica o nome do formulário PDF gerado.

#### Parâmetros adicionais {#additional-parameters}

* *Raiz* do conteúdo: Especifica o caminho para a pasta no repositório onde os fragmentos ou imagens usados no modelo XDP de entrada são armazenados.
* *Enviar URL*: Especifica o URL de envio padrão para o formulário PDF gerado.
* *Local*: Especifica a localidade padrão para o formulário PDF gerado.
* *Versão* do Acrobat: Especifica a versão de destino do Acrobat para o formulário PDF gerado.
* *PDF* marcado: Especifica se o PDF gerado deve ser acessível.
* *Documento* XCI: Especifica o caminho para o arquivo XCI.

## Saída {#output}

O Fluxo de trabalho Gerar PDF não interativo é um encapsulador em torno da `generatePDFOutput` API do serviço de saída. É usado para gerar documentos PDF não interativos do modelo XDP e do xml de dados.

### Gerar fluxo de trabalho de saída de PDF não interativo   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. Arraste o fluxo de trabalho Gerar saída de PDF não interativa na guia Forms Workflow no Sidekick.
1. Clique com o duplo na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, documentos de saída e parâmetros adicionais e clique em **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents-3}

* *Arquivo* de modelo: Especifica o local do modelo XDP. É um campo obrigatório.

* *Documento* de dados: Especifica o local do xml de dados que precisa ser unido ao modelo.

#### Documento de saída {#output-document}

*Documento* de saída: Especifica o nome do formulário PDF gerado.

#### Parâmetros adicionais {#additional-parameters-1}

* *Raiz* do conteúdo: Especifica o caminho para a pasta no repositório onde os fragmentos ou imagens usados no modelo XDP de entrada são armazenados.
* *Local*: Especifica a localidade padrão para o formulário PDF gerado.
* *Versão* do Acrobat: Especifica a versão de destino do Acrobat para o formulário PDF gerado.
* PDF linearizado: Especifica se o PDF gerado deve ser otimizado para visualização na Web.
* *PDF* marcado: Especifica se o PDF gerado deve ser acessível.
* *Documento* XCI: Especifica o caminho para o arquivo XCI.

