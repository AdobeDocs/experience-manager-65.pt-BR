---
title: Gerar Documento de registro para formulários adaptáveis
seo-title: Gerar Documento de registro para formulários adaptáveis
description: Explica como você pode gerar um modelo para um documento de registro (DoR) para formulários adaptáveis.
seo-description: Explica como você pode gerar um modelo para um documento de registro (DoR) para formulários adaptáveis.
uuid: 2dc7e0de-fff9-43fa-9426-e9b047eb2595
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ce65cb5f-94ec-4423-9fa9-d617e9703091
docset: aem65
translation-type: tm+mt
source-git-commit: fa3d5923784a8d89e2b440412d2b88790de3e39e
workflow-type: tm+mt
source-wordcount: '2663'
ht-degree: 3%

---


# Gerar Documento de registro para formulários adaptáveis{#generate-document-of-record-for-adaptive-forms}

## Visão geral {#overview}

Depois de enviar um formulário, os clientes geralmente desejam manter um registro, em formato impresso ou em formato de documento, das informações que preencheram no formulário para referência futura. Isso é conhecido como um documento de registro.

Este artigo explica como gerar um documento de registro para formulários adaptáveis.

>[!NOTE]
>
>A geração automática de documento de registro não é suportada em formulários adaptativos baseados em XFA. Entretanto, você pode usar o XDP usado para criar o formulário adaptável como documento de registro.

## Tipos de formulário adaptáveis e seus documentos de registro {#adaptive-form-types-and-their-documents-of-record}

Ao criar um formulário adaptável, é possível selecionar um modelo de formulário. Suas opções são:

* [Modelos](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)de formulárioPermite selecionar um modelo XFA para o formulário adaptável. Ao selecionar um modelo XFA, você pode usar o arquivo XDP associado para o documento de registro, conforme descrito acima.

* [SCHEMA](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)XML Permite selecionar uma definição de schema XML para o formulário adaptável. Ao selecionar um schema XML para o formulário adaptável, é possível:

   * Associe um modelo XFA ao documento de registro. Certifique-se de que o modelo XFA associado use o mesmo schema XML do formulário adaptável
   * Gerar automaticamente documento de registro

* NenhumPermite criar um formulário adaptável sem um modelo de formulário. O documento de registro é gerado automaticamente para o formulário adaptável.

Ao selecionar um modelo de formulário, configure o documento de registro usando as opções disponíveis em Documento de Gravar configuração de modelo. See [Document of Record Template Configuration](#document-of-record-template-configuration).

## Documento de registro gerado automaticamente {#automatically-generated-document-of-record}

Um documento de registro permite que seus clientes mantenham uma cópia do formulário enviado para fins de impressão. Quando você gera automaticamente um documento de registro, toda vez que você altera o formulário, seu documento de registro é atualizado imediatamente. Por exemplo, você remove o campo de idade para clientes que selecionam Estados Unidos da América como seu país. Quando esses clientes geram um documento de registro, o campo de idade não é visível para eles no documento de registro.

O documento de registro gerado automaticamente tem as seguintes vantagens:

* Ele cuida do vínculo de dados.
* Oculta automaticamente os campos marcados como excluídos do documento de registro no momento do envio. Não é necessário nenhum esforço adicional.
* Ele economiza tempo para projetar o documento do modelo de registro.
* Ele permite que você experimente estilos e aparência diferentes usando diferentes modelos base e escolha o melhor estilo e aparência para o Documento de Registro. As aparências de estilo são opcionais e, se você não especificar estilos, os estilos do sistema serão definidos como padrão.
* Isso garante que qualquer alteração no formulário seja refletida imediatamente no documento do registro.

## Componentes para gerar automaticamente um documento de registro {#components-to-automatically-generate-a-document-of-record}

Para gerar um documento de registro para formulários adaptáveis, você precisa dos seguintes componentes:

**Formulário** adaptável para o qual você deseja gerar um documento de registro.

**Modelo base (recomendado)** modelo XFA (arquivo XDP) criado no AEM Designer. O modelo básico é usado para especificar informações de estilo e marca para o documento do modelo de registro.

Consulte Modelo [base de um documento de registro](#base-template-of-a-document-of-record)

>[!NOTE]
>
>O modelo básico de um documento de registro também é chamado de meta-modelo de um documento de registro.

**Documento do modelo** de registro XFA modelo (arquivo XDP) gerado de um formulário adaptável.

See [Document of Record Template Configuration](#document-of-record-template-configuration).

**Informações de dados** do formulário preenchidas por um usuário no formulário adaptável. Ele se funde com o documento do modelo de registro para gerar o documento de registro.

## Mapeamento de elementos de formulário adaptáveis {#mapping-of-adaptive-form-elements}

As seções a seguir descrevem como os elementos de formulário adaptáveis aparecem no documento do registro.

### Fields {#fields}

<table>
 <tbody>
  <tr>
   <th>Componente de formulário adaptável</th>
   <th>Componente XFA correspondente</th>
   <th>Incluído por padrão no documento do modelo de registro?</th>
   <th>Notas</th>
  </tr>
  <tr>
   <td>Botão</td>
   <td>Botão</td>
   <td>falso</td>
   <td> </td>
  </tr>
  <tr>
   <td>Caixa de seleção</td>
   <td>Caixa de seleção</td>
   <td>verdadeiro</td>
   <td> </td>
  </tr>
  <tr>
   <td>Seletor de data</td>
   <td>Campo de data/hora</td>
   <td>verdadeiro</td>
   <td> </td>
  </tr>
  <tr>
   <td>Lista suspensa</td>
   <td>Lista suspensa</td>
   <td>verdadeiro</td>
   <td> </td>
  </tr>
  <tr>
   <td>Rabiscar a assinatura</td>
   <td>Gráfico de assinatura</td>
   <td>verdadeiro</td>
   <td> </td>
  </tr>
  <tr>
   <td>Caixa numérica</td>
   <td>Campo numérico</td>
   <td>verdadeiro</td>
   <td> </td>
  </tr>
  <tr>
   <td>Caixa de senha</td>
   <td>Campo de senha</td>
   <td>falso</td>
   <td> </td>
  </tr>
  <tr>
   <td>Botão de opção</td>
   <td>Botão de opção</td>
   <td>verdadeiro</td>
   <td> </td>
  </tr>
  <tr>
   <td>Caixa de texto</td>
   <td>Campo de texto</td>
   <td>verdadeiro</td>
   <td> </td>
  </tr>
  <tr>
   <td>Botão de redefinição</td>
   <td>Botão Redefinir</td>
   <td>falso</td>
   <td> </td>
  </tr>
  <tr>
   <td>Botão Enviar</td>
   <td><p>Botão Submeter por email</p> <p>Botão Submeter por HTTP</p> </td>
   <td>falso</td>
   <td> </td>
  </tr>
  <tr>
   <td>Termos e condições</td>
   <td> </td>
   <td>verdadeiro</td>
   <td> </td>
  </tr>
  <tr>
   <td>Anexo de arquivo</td>
   <td> </td>
   <td>falso</td>
   <td>Não disponível no documento do modelo de registro. Disponível somente em documento de registro por meio de anexos.</td>
  </tr>
 </tbody>
</table>

### Containers {#containers}

<table>
 <tbody>
  <tr>
   <th>Componente de formulário adaptável</th>
   <th>Componente XFA correspondente</th>
   <th>Notas</th>
  </tr>
  <tr>
   <td>Painel<br /> </td>
   <td>Subformulário<br /> </td>
   <td>O painel repetível mapeia para subformulário repetível.</td>
  </tr>
 </tbody>
</table>

### Componentes estáticos {#static-components}

| Componente de formulário adaptável | Componente XFA correspondente | Notas |
|---|---|---|
| Imagem | Imagem | Os componentes TextDraw e Image, vinculados ou não, sempre aparecem no documento de registro de um formulário adaptável baseado em XSD, a menos que seja excluído usando o documento das configurações de registro. |
| Texto | Texto |

>[!NOTE]
>
>Na interface clássica, você obtém guias diferentes para editar propriedades de campos.

### Tabelas {#tables}

Os componentes adaptáveis da tabela de formulários, como cabeçalho, rodapé e mapa de linhas, para os componentes XFA correspondentes. Você pode mapear painéis repetíveis em tabelas em documento de registro.

## Modelo de base de um documento de registro {#base-template-of-a-document-of-record}

O modelo base fornece informações de estilo e aparência ao documento do registro. Permite personalizar a aparência padrão do documento de registro gerado automaticamente. Por exemplo, você deseja adicionar o logotipo da empresa no cabeçalho e as informações de copyright no rodapé do documento de registro. A página principal do modelo base é usada como uma página principal para o documento do modelo de registro. A página principal pode ter informações como cabeçalho de página, rodapé de página e número de página que você pode aplicar ao documento de registro. Você pode aplicar essas informações ao documento de registro usando o modelo básico para a geração automática do documento de registro. O uso do modelo base permite alterar as propriedades padrão dos campos.

Siga as convenções [de modelo](#base-template-conventions) básico ao projetar o modelo base.

## Convenções de modelo básico {#base-template-conventions}

Um modelo base é usado para definir cabeçalho, rodapé, estilo e aparência para um documento de registro. O cabeçalho e o rodapé podem incluir informações como o logotipo da empresa e o texto de direitos autorais. A primeira página principal no modelo base é copiada e usada como uma página principal para o documento do registro, que contém cabeçalho, rodapé, número de página ou qualquer outra informação que deve aparecer em todas as páginas no documento do registro. Se você estiver usando um modelo base que não esteja em conformidade com as convenções de modelo base, a primeira página principal do modelo base ainda será usada no documento do modelo de registro. É altamente recomendável que você crie seu modelo base de acordo com suas convenções e o use para a geração automática do documento de registro.

**Convenções de página principais**

* No modelo base, é necessário nomear o subformulário raiz como `AF_METATEMPLATE` e a página principal como `AF_MASTERPAGE`.

* A página principal com o nome `AF_MASTERPAGE` localizado no subformulário `AF_METATEMPLATE` raiz recebe preferência pela extração de informações de cabeçalho, rodapé e estilo.

* Se `AF_MASTERPAGE` estiver ausente, a primeira página principal presente no modelo base será usada.

**Convenções de estilo para campos**

* Para aplicar estilo aos campos no documento de registro, o modelo base fornece campos localizados no subformulário `AF_FIELDSSUBFORM` sob o subformulário `AF_METATEMPLATE` raiz.

* As propriedades desses campos são aplicadas aos campos no documento de registro. Esses campos devem seguir a convenção de `AF_<name of field in all caps>_XFO` nomenclatura. Por exemplo, o nome do campo para a caixa de seleção deve ser `AF_CHECKBOX_XFO`.

Para criar um modelo base, faça o seguinte no AEM Designer.

1. Clique em **Arquivo > Novo**.
1. Selecione a opção **Com base em um modelo** .

1. Selecione **Forms - Documento da categoria de registro** .
1. Selecione Modelo **Base** DoR.
1. Clique em **Avançar** e forneça as informações necessárias.

1. (Opcional) Modifique o estilo e a aparência dos campos que você deseja aplicar aos campos no documento de registro.
1. Salve o formulário.

Agora é possível usar o formulário salvo como modelo base para o documento de registro.
Não modifique ou remova quaisquer scripts presentes no modelo base.

**Modificando modelo base**

* Se você não estiver aplicando nenhum estilo sobre os campos no modelo base, é aconselhável remover esses campos do modelo base para que quaisquer atualizações no modelo base sejam automaticamente coletadas.
* Ao modificar o modelo base, não remova, adicione ou modifique scripts.

>[!NOTE]
>
>Projete modelo base usando convenções e seguindo rigorosamente as etapas acima.

## Documento de configuração modelo de registro {#document-of-record-template-configuration}

Configure o documento do modelo de registro do formulário para permitir que os clientes baixem uma cópia fácil de imprimir do formulário enviado. Um arquivo XDP serve como o documento do modelo de registro. O documento de download de clientes de registro é formatado de acordo com o layout especificado no arquivo XDP.

Execute as seguintes etapas para configurar um documento de registro para formulários adaptáveis:

1. Em AEM instância do autor, clique em **Forms > Forms e Documentos.**
1. Selecione um formulário e clique em Propriedades **da** Visualização.
1. Na janela Propriedades, toque em Modelo **de**formulário.
Também é possível selecionar um modelo de formulário ao criar um formulário.

   >[!NOTE]
   >
   >Na guia Modelo de formulário, selecione **Schema** ou **Nenhum** no menu suspenso **Selecionar** . **[!UICONTROL O documento de registro não é compatível com formulários baseados em XFA ou adaptáveis com Modelo de formulário como modelo de formulário.]**

1. Na seção Documento de Configuração de modelo de registro da guia Modelo de formulário, selecione uma das seguintes opções.

   **Nenhum** Selecione essa opção se não quiser configurar o documento de registro para o formulário.

   **Associar modelo de formulário como Documento de modelo** de registro Selecione esta opção se você tiver um arquivo XDP que deseja usar como modelo para o documento de registro. Ao selecionar essa opção, todos os arquivos XDP disponíveis no repositório AEM Forms serão exibidos. Selecione o arquivo apropriado.

   O arquivo XDP selecionado é associado ao formulário adaptável.

   **Gerar Documento de registro** Selecione esta opção para usar um arquivo XDP como modelo base para definir o estilo e a aparência do documento de registro. Ao selecionar essa opção, todos os arquivos XDP disponíveis no repositório AEM Forms serão exibidos. Selecione o arquivo apropriado.

   >[!NOTE]
   >
   >Verifique se o schema usado para criar formulários adaptáveis e schemas (schema de dados) do formulário XFA são os mesmos se:
   >
   >
   >
   >    * Seu formulário adaptável é baseado em schema
   >    * Você está usando a opção **Associar modelo de formulário como o Documento do modelo** de registro para o documento do registro


1. Clique em **Concluído.**

## Personalizar as informações de marca em documento do registro {#customize-the-branding-information-in-document-of-record}

Ao gerar um documento de registro, você pode alterar as informações de marca do documento de registro na guia Documento de registro. A guia Documento de registro inclui opções como logotipo, aparência, layout, cabeçalho e rodapé, aviso e se você deseja incluir ou não opções de caixa de seleção e botão de opção não selecionadas.

Para localizar as informações de marca inseridas na guia Documento de registro, verifique se a localidade do navegador está definida adequadamente. Para personalizar as informações de marca do documento de registro, execute as seguintes etapas:

1. Selecione um painel (painel raiz) no documento de registro e toque em ![configurar](assets/configure.png).
1. Toque em ![dortab](assets/dortab.png). A guia Documento de registro é exibida.
1. Selecione o modelo padrão ou um modelo personalizado para renderizar o documento de registro. Se você selecionar o modelo padrão, uma pré-visualização em miniatura do documento de registro será exibida abaixo do menu suspenso Modelo.

   ![modelo de marca](assets/brandingtemplate.png)

   Se você optar por selecionar um modelo personalizado, navegue por um XDP selecionado em seu servidor AEM Forms. Se você quiser usar um modelo que ainda não esteja no servidor AEM Forms, primeiro carregue o XDP no servidor AEM Forms.

1. Com base na seleção de um modelo padrão ou personalizado, algumas ou todas as propriedades a seguir são exibidas na guia Documento de registro. Especifique-os adequadamente:

   * **Imagem** do logotipo: Você pode optar por usar a imagem do logotipo no formulário adaptável, escolher uma no DAM ou fazer upload de uma no computador.
   * **Título do formulário**
   * **Texto do cabeçalho**
   * **Rótulo do aviso**
   * **Aviso**
   * **Texto do aviso**
   * **Cor** do destaque: A cor na qual o texto do cabeçalho e as linhas separadoras são renderizados no documento ou no PDF do registro
   * **Família** de fontes: Família de fontes do texto no documento de gravar PDF
   * **Para componentes de caixa de seleção e botão de opção, mostrar apenas os valores selecionados**
   * **Separador para vários valores selecionados**
   * **Incluir objetos de formulário que não estão vinculados ao modelo de dados**
   * **Excluir campos ocultos do documento de registro**
   * **Ocultar descrição de painéis**

   >[!NOTE]
   >
   >Se você estiver usando um modelo de formulário adaptável criado com uma versão do Designer anterior à 6.3, para que as propriedades Cor do destaque e Família de fontes funcionem, verifique se o seguinte está presente no modelo de formulário adaptável sob o subformulário raiz:

   ```xml
   <proto>
   <font typeface="Arial"/>
   <fill>
   <color value="4,166,203"/>
   </fill>
   <edge>
   <color value="4,166,203"/>
   </edge>
   </proto>
   ```

1. Para salvar as alterações de marca, toque em Concluído.

## Layouts de tabela e coluna para painéis em Documento de Registro {#table-and-column-layouts-for-panels-in-document-of-record}

Seu formulário adaptável pode ser longo, com vários campos de formulário. Talvez você não queira salvar um documento de registro como uma cópia exata do formulário adaptável. Agora é possível escolher um layout de tabela ou coluna para salvar um ou mais painéis de formulário adaptáveis no documento de gravar PDF.

Antes de gerar um documento de registro, nas configurações de um painel, selecione Layout para o Documento de registro desse painel como Tabela ou Coluna. Os campos no painel se organizam de acordo no documento de registro.

![Campos em um painel renderizado em um layout de tabela no documento de registro](assets/dortablelayout.png)

Campos em um painel renderizado em um layout de tabela no documento de registro

![Campos em um painel renderizado em um layout de coluna no documento de registro](assets/dorcolumnlayout.png)

Campos em um painel renderizado em um layout de coluna no documento de registro

## Documento das configurações de registro {#document-of-record-settings}

O documento das configurações de registro permite que você escolha as opções que deseja incluir no documento de registro. Por exemplo, um banco aceita nome, idade, número de segurança social e número de telefone em um formulário. O formulário gera um número de conta bancária e detalhes da sucursal. Você pode optar por exibir somente o nome, o número da previdência social, a conta bancária e os detalhes da ramificação no documento do registro.

O documento das configurações de registro de um componente está disponível em suas propriedades. Para acessar as propriedades de um componente, selecione o componente e clique em ![cmppr](assets/cmppr.png) na sobreposição. As propriedades são listadas na barra lateral e você pode encontrar as seguintes configurações nela.

**Configurações de nível de campo**

* **Excluir Do Documento Do Registro**: A definição da propriedade true exclui o campo do documento de registro. Esta é uma propriedade com script chamada `excludeFromDoR`. Seu comportamento depende de **Excluir campos do DoR se a propriedade de nível de formulário oculta** .

* **Exibir painel como tabela:** A definição da propriedade exibe o painel como tabela no documento de registro se o painel tiver menos de 6 campos nele. Aplicável somente para painel.
* **Excluir título do Documento de Registro:** A configuração da propriedade exclui o título do painel/tabela do documento de registro. Aplicável apenas para painel e tabela.
* **Excluir descrição do Documento do Registro:** A definição da propriedade exclui a descrição do painel/tabela do documento de registro. Aplicável apenas para painel e tabela.

**Configurações de nível de formulário**

* **Incluir campos não vinculados no DoR:** A configuração da propriedade inclui campos não vinculados do formulário adaptativo baseado em Schema, em documento de registro. Por padrão, é verdadeiro.
* **Excluir campos do DoR se ocultos:** A definição da propriedade substitui o comportamento da propriedade de nível de campo &quot;Excluir do Documento do Registro&quot; quando não é verdadeiro. Se os campos estiverem ocultos no momento do envio do formulário, serão excluídos do documento do registro se a propriedade for definida como verdadeira, desde que a propriedade &quot;Excluir do Documento do registro&quot; não esteja definida.

## Considerações principais ao trabalhar com o documento de registro {#key-considerations-when-working-with-document-of-record}

Lembre-se das seguintes considerações e limitações ao trabalhar no documento de registro para formulários adaptáveis.

* O documento de modelos de registro não suporta Rich Text. Portanto, qualquer rich text no formulário adaptativo estático ou nas informações preenchidas pelo usuário final aparece como texto sem formatação no documento do registro.
* Os fragmentos de documento em um formulário adaptável não aparecem no documento de registro. No entanto, os fragmentos de formulário adaptáveis são suportados.
* O vínculo de conteúdo em documento de registro gerado para o formulário adaptativo baseado em Schema XML não é suportado.
* A versão localizada do documento do registro é criada sob demanda para uma localidade quando o usuário solicita a renderização do documento do registro. A localização do documento do registro ocorre junto com a localização da forma adaptativa. Para obter mais informações sobre a localização do documento de formulários de registro e adaptativos, consulte [Usar AEM fluxo de trabalho de tradução para localizar formulários adaptáveis e documento de registro](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

