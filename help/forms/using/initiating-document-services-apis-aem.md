---
title: Iniciar APIs de serviços de documento AEM fluxo de trabalho
seo-title: Initiate Document Services APIs from AEM Workflow
description: Saiba como invocar AEM serviços de documento no DDX ou entradas fornecidas. Veja também como converter PDF para PDF/A
seo-description: Learn how to invoke AEM Document services on DDX or supplied inputs. Also see hwo to convert PDF to PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
exl-id: 123087a2-9d09-4579-9185-2ccd7d25bf8d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 0%

---

# Iniciar APIs de serviços de documento AEM fluxo de trabalho  {#initiate-document-services-apis-from-aem-workflow}

## Assembler {#assembler}

O AEM Forms fornece workflows personalizados para chamar as seguintes APIs de serviço do Assembler:

* **invocar**: Chama as operações especificadas no DDX de entrada nas entradas fornecidas.
* **toPDFA**: Converte o documento PDF de entrada em documento PDF/A.

### Chamar fluxo de trabalho DDX {#invoke-ddx-workflow}

O **Chamar DDX** workflow chama a variável `Invoke` API do serviço Assembler, que pode ser usada para montar ou desmontar documentos, adicionar marca d&#39;água a um PDF e assim por diante.

1. Arraste o **[!UICONTROL Chamar DDX]** etapa do fluxo de trabalho na guia Forms Workflow no Sidekick.
1. Clique duas vezes na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure os documentos de entrada, as opções de ambiente e os documentos de saída e clique em **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents}

O fluxo de trabalho Invoke DDX requer os seguintes documentos de entrada:

* **DDX**: É uma entrada obrigatória para a etapa de fluxo de trabalho Invoke DDX e pode ser especificada ao selecionar uma das seguintes opções no menu suspenso de entrada DX.

   * *Relativo À Carga*: O arquivo de entrada DDX é relativo à pasta de carga do item de fluxo de trabalho.
   * *Usar carga*: A carga útil do item de fluxo de trabalho é usada como o documento DDX de entrada.
   * *Caminho absoluto*: O caminho absoluto para o documento DDX no repositório CRX.

* **Criar mapa a partir do PayLoad**: Quando selecionada, todos os documentos na pasta de carga são adicionados ao Mapa do Documento de Entrada para a `invoke` API no Assembler. O nome do nó de cada documento é usado como uma chave no mapa.

* **Mapa do Documento de Entrada**: Especifica o Mapa do Documento de Entrada. Você pode adicionar qualquer número de entradas, onde cada entrada especifica a chave do documento no mapa e a origem do documento.

#### Opções de ambiente {#environment-options}

A guia Opções de ambiente permite que você defina várias opções de processamento para a API de chamada.

* *Nível do Log de Trabalho*: Especifica o nível de log para os logs de processamento.
* *Validar somente*: Verifica a validade do DDX de entrada.

* *Falha no Erro*: Especifica se a chamada para o serviço Assembler deve falhar em caso de erro. O valor padrão é Falso.

#### Documentos de saída {#output-documents}

Dependendo do DDX de entrada, a API de chamada pode produzir vários documentos de saída. A guia Documentos de saída permite que você selecione onde o documento de saída será salvo.

1. *Salvar saída na carga*: Salva documentos de saída na pasta carga ou substitui a carga, se a carga for um arquivo.
1. *Mapa do Documento de Saída*: Permite especificar explicitamente onde salvar cada documento de saída adicionando uma entrada por documento de saída. Cada entrada especifica o documento e onde salvá-lo. Um documento de saída pode substituir a carga útil ou ser salvo na pasta da carga útil. É útil quando há vários documentos de saída.

1. *Log de trabalho*: Especifica onde salvar o documento de log de tarefas, que é útil em falhas de solução de problemas.

### Converter em fluxo de trabalho PDF/A {#convert-to-pdf-a-workflow}

A etapa de fluxo de trabalho Converter em PDF/A chama a variável `toPDFA` API do serviço Assembler. Ele é usado para converter documentos PDF para documentos compatíveis com PDF/A.

1. Arraste o **[!UICONTROL ConvertToPDFA]** etapa do fluxo de trabalho na guia Forms Workflow no Sidekick.

1. Clique duas vezes na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, opções de conversão e documentos de saída e clique em **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents-1}

Especifique a origem do documento para conversão em um documento compatível com PDF/A de uma das seguintes maneiras.

* *Relativo À Carga*: O documento de entrada é relativo à pasta de carga do item de fluxo de trabalho.
* *Usar carga*: A carga útil do item de fluxo de trabalho é usada como documento de entrada.
* *Caminho absoluto*: O caminho absoluto do documento de entrada no repositório CRX.

#### Opções de conversão {#conversion-options}

As Opções de conversão permitem especificar opções que alteram o processo de conversão de PDF/A.

* *Conformidade* : Especifica o padrão PDF/A ao qual o PDF de saída/A deve estar em conformidade.
* *Nível de Resultado* : Especifica o nível de log a ser usado para logs de conversão de PDF/A.
* *Assinaturas* : Especifica como as assinaturas no documento de entrada devem ser processadas durante a conversão.
* *Espaço da cor* : Especifica o espaço de cores predefinido a ser usado para o documento PDF/A de saída.
* *Verificar* Conversão: Especifica se o documento PDF/A convertido deve ser verificado para conformidade PDF/A após a conversão.
* *Nível do Log de Trabalho* : Especifica o nível de log a ser usado para logs de processamento.

* *Esquema de extensão de metadados* : Especifica o caminho para o esquema de extensão de metadados a ser usado para XMP propriedades nos metadados do documento do PDF.

#### Documentos de saída {#output-documents-1}

A guia Documentos de saída permite especificar o destino dos documentos de saída

* *Documento PDFA*: Especifica o local onde o documento PDF/A convertido é salvo. Ele pode substituir o documento de carga útil ou ser salvo na pasta de carga útil.
* *Log de conversão*: Especifica o local onde os logs de conversão são salvos. Ele pode substituir o documento de carga ou pode ser salvo na pasta de carga útil.

## Forms {#forms}

O fluxo de trabalho Renderizar formulário PDF é um wrapper `renderPDFForm` API de serviço do Forms para criar um formulário PDF usando um template XDP e um xml de dados.

### Renderizar fluxo de trabalho do formulário de PDF {#render-pdf-form-workflow}

1. Arraste a etapa de fluxo de trabalho Renderizar formulário PDF na guia Forms Workflow no Sidekick.
1. Clique duas vezes na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, documentos de saída e parâmetros adicionais e clique em **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents-2}

* *Arquivo de modelo*: Especifica o local do modelo XDP. É um campo obrigatório.

* *Documento de dados*: Especifica o local do xml de dados que precisa ser unido ao modelo.

#### Documentos de saída {#output-documents-2}

* *Documento de saída*: - Especifica o nome do formulário PDF gerado.

#### Parâmetros adicionais {#additional-parameters}

* *Raiz do conteúdo*: Especifica o caminho para a pasta no repositório onde os fragmentos ou imagens usados no modelo XDP de entrada são armazenados.
* *Enviar Url*: Especifica o URL de envio padrão para o formulário PDF gerado.
* *Localidade*: Especifica o local padrão para o formulário PDF gerado.
* *Versão do Acrobat*: Especifica a versão de destino do Acrobat para o formulário PDF gerado.
* *PDF com tags*: Especifica se o PDF gerado deve ser acessível.
* *Documento XCI*: Especifica o caminho para o arquivo XCI.

## Saída {#output}

O Fluxo de Trabalho Gerar PDF não interativo é um wrapper ao redor `generatePDFOutput` API do serviço de saída. Ele é usado para gerar documentos PDF não interativos do template XDP e do xml de dados.

### Gerar fluxo de trabalho de PDF Output não interativo   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. Arraste o fluxo de trabalho Gerar saída de PDF não interativa na guia Forms Workflow no Sidekick.
1. Clique duas vezes na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, documentos de saída e parâmetros adicionais e clique em **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents-3}

* *Arquivo de modelo*: Especifica o local do modelo XDP. É um campo obrigatório.

* *Documento de dados*: Especifica o local do xml de dados que precisa ser unido ao modelo.

#### Documento de saída {#output-document}

*Documento de saída*: Especifica o nome do formulário PDF gerado.

#### Parâmetros adicionais {#additional-parameters-1}

* *Raiz do conteúdo*: Especifica o caminho para a pasta no repositório onde os fragmentos ou imagens usados no modelo XDP de entrada são armazenados.
* *Localidade*: Especifica o local padrão para o formulário PDF gerado.
* *Versão do Acrobat*: Especifica a versão de destino do Acrobat para o formulário PDF gerado.
* PDF linearizado: Especifica se deve-se otimizar o PDF gerado para visualização da Web.
* *PDF com tags*: Especifica se o PDF gerado deve ser acessível.
* *Documento XCI*: Especifica o caminho para o arquivo XCI.
