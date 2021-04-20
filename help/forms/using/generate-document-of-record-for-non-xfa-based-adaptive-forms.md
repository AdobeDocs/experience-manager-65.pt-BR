---
title: Gerar documento de registro para formulários adaptáveis
seo-title: Gerar documento de registro para formulários adaptáveis
description: Explica como você pode gerar um modelo para um documento de registro (DoR) para formulários adaptáveis.
seo-description: Explica como você pode gerar um modelo para um documento de registro (DoR) para formulários adaptáveis.
uuid: 2dc7e0de-fff9-43fa-9426-e9b047eb2595
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ce65cb5f-94ec-4423-9fa9-d617e9703091
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2665'
ht-degree: 3%

---


# Gerar Documento de Registro para formulários adaptáveis{#generate-document-of-record-for-adaptive-forms}

## Visão geral {#overview}

Depois de enviar um formulário, os clientes geralmente desejam manter um registro, em formato impresso ou de documento, das informações que preencheram no formulário para referência futura. Isso é chamado de documento de registro.

Este artigo explica como gerar um documento de registro para formulários adaptáveis.

>[!NOTE]
>
>A geração automática de documento de registro não é compatível com formulários adaptáveis baseados em XFA. No entanto, você pode usar o XDP usado para criar o formulário adaptável como documento de registro.

## Tipos de formulário adaptável e seus documentos de registro {#adaptive-form-types-and-their-documents-of-record}

Ao criar um formulário adaptável, é possível selecionar um modelo de formulário. Suas opções são:

* [](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
Modelos de formulárioPermite selecionar um modelo XFA para seu formulário adaptável. Ao selecionar um modelo XFA, você pode usar o arquivo XDP associado para o documento de registro, conforme descrito acima.

* [Esquema ](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
XML Permite selecionar uma definição de esquema XML para o formulário adaptável. Ao selecionar um esquema XML para o formulário adaptável, é possível:

   * Associe um modelo XFA para o documento de registro. Certifique-se de que o modelo XFA associado use o mesmo esquema XML que o formulário adaptável
   * Gerar automaticamente documento de registro

* Nenhum
Permite criar um formulário adaptável sem um modelo de formulário. O documento de registro é gerado automaticamente para o formulário adaptável.

Ao selecionar um modelo de formulário, configure o documento de registro usando as opções disponíveis em Document of Record Template Configuration. Consulte [Documento de configuração de modelo de registro](#document-of-record-template-configuration).

## Documento gerado automaticamente do registro {#automatically-generated-document-of-record}

Um documento de registro permite que seus clientes mantenham uma cópia do formulário enviado para fins de impressão. Quando um documento de registro é gerado automaticamente, sempre que você altera o formulário, o documento de registro é atualizado imediatamente. Por exemplo, você remove o campo de idade dos clientes que selecionam os Estados Unidos da América como seu país. Quando esses clientes geram um documento de registro, o campo idade não é visível para eles no documento de registro.

O documento de registro gerado automaticamente tem as seguintes vantagens:

* Ela cuida do vínculo de dados.
* Ele oculta automaticamente os campos marcados como excluídos do documento de registro no momento do envio. Não é necessário qualquer esforço adicional.
* Ele economiza tempo para projetar o documento do modelo de registro.
* Ele permite que você experimente diferentes estilos e aparência usando diferentes modelos base e escolha o melhor estilo e aparência para o Documento de registro. As aparências de estilo são opcionais e, se você não especificar o estilo, os estilos do sistema serão definidos como padrão.
* Garante que qualquer alteração no formulário seja refletida imediatamente no documento de registro.

## Componentes para gerar automaticamente um documento de registro {#components-to-automatically-generate-a-document-of-record}

Para gerar um documento de registro para formulários adaptáveis, você precisa dos seguintes componentes:

**Adaptive** formAdaptive form para o qual você deseja gerar um documento de registro.

**Modelo base (recomendado)** Modelo XFA (arquivo XDP) criado AEM Designer. O modelo base é usado para especificar informações de estilo e identidade visual para o documento de modelo de registro.

Consulte [Modelo base de um documento de registro](#base-template-of-a-document-of-record)

>[!NOTE]
>
>O modelo base de um documento de registro também é chamado de metamodelo de um documento de registro.

**Documento de** template de registroModelo XFA (arquivo XDP) gerado de um formulário adaptável.

Consulte [Documento de configuração de modelo de registro](#document-of-record-template-configuration).

**Dados** do formulárioInformações preenchidas por um usuário no formulário adaptável. Ele se mescla com o documento do template de registro para gerar o documento de registro.

## Mapeamento de elementos de formulário adaptáveis {#mapping-of-adaptive-form-elements}

As seções a seguir descrevem como os elementos de formulário adaptáveis aparecem no documento de registro.

### Fields {#fields}

<table>
 <tbody>
  <tr>
   <th>Componente de formulário adaptável</th>
   <th>Componente XFA correspondente</th>
   <th>Incluído por padrão no documento de registro Modelo?</th>
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
   <td>Scribble de assinatura</td>
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
   <td>Não disponível no documento do modelo de registro. Disponível apenas no documento de registro através de anexos.</td>
  </tr>
 </tbody>
</table>

### Contêineres {#containers}

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
| Imagem | Imagem | Os componentes TextDraw e Image, vinculados ou não, sempre aparecem no documento de registro para um formulário adaptável baseado em XSD, a menos que sejam excluídos usando as configurações de documento de registro. |
| Texto | Texto |

>[!NOTE]
>
>Na interface clássica, você obtém guias diferentes para editar as propriedades dos campos.

### Tabelas {#tables}

Os componentes da tabela de formulários adaptáveis, como cabeçalho, rodapé e mapa de linhas para os componentes XFA correspondentes. Você pode mapear painéis repetitivos para tabelas no documento de registro.

## Modelo base de um documento de registro {#base-template-of-a-document-of-record}

O modelo base fornece informações de estilo e aparência para o documento de registro. Permite personalizar a aparência padrão do documento de registro gerado automaticamente. Por exemplo, você deseja adicionar o logotipo da empresa no cabeçalho e as informações de direitos autorais no rodapé do documento de registro. A página principal do modelo base é usada como uma página principal para o documento de modelo de registro. A página principal pode ter informações como cabeçalho de página, rodapé de página e número de página que você pode aplicar ao documento de registro. Você pode aplicar essas informações ao documento de registro usando o modelo base para a geração automática de documento de registro. O uso do template base permite alterar as propriedades padrão dos campos.

Siga [Convenções de modelo base](#base-template-conventions) ao criar o modelo base.

## Convenções de modelo base {#base-template-conventions}

Um modelo base é usado para definir o cabeçalho, o rodapé, o estilo e a aparência de um documento de registro. O cabeçalho e o rodapé podem incluir informações como o logotipo da empresa e o texto de direitos autorais. A primeira página principal no modelo base é copiada e usada como uma página principal para o documento de registro, que contém cabeçalho, rodapé, número de página ou qualquer outra informação que deve aparecer em todas as páginas no documento de registro. Se você estiver usando um modelo base que não está em conformidade com as convenções do modelo base, a primeira página principal do modelo base ainda será usada no documento de modelo de registro. É altamente recomendável criar seu modelo base de acordo com suas convenções e usá-lo para a geração automática de documento de registro.

**Convenções de página principais**

* No modelo base, você deve nomear o subformulário raiz como `AF_METATEMPLATE` e a página principal como `AF_MASTERPAGE`.

* A página principal com o nome `AF_MASTERPAGE` localizado no subformulário raiz `AF_METATEMPLATE` recebe preferência por extrair informações de cabeçalho, rodapé e estilo.

* Se `AF_MASTERPAGE` estiver ausente, a primeira página principal presente no modelo base será usada.

**Convenções de estilo para campos**

* Para aplicar estilo aos campos no documento de registro, o modelo base fornece campos localizados no subformulário `AF_FIELDSSUBFORM` sob o subformulário raiz `AF_METATEMPLATE`.

* As propriedades desses campos são aplicadas aos campos no documento de registro. Esses campos devem seguir a convenção de nomenclatura `AF_<name of field in all caps>_XFO`. Por exemplo, o nome do campo para a caixa de seleção deve ser `AF_CHECKBOX_XFO`.

Para criar um modelo base, faça o seguinte no AEM Designer.

1. Clique em **Arquivo > Novo**.
1. Selecione a opção **Baseado em um template**.

1. Selecione a categoria **Forms - Document of Record**.
1. Selecione **Modelo Base DoR**.
1. Clique em **Next** e forneça as informações necessárias.

1. (Opcional) Modifique o estilo e a aparência dos campos que deseja aplicar nos campos do documento de registro.
1. Salve o formulário.

Agora você pode usar o formulário salvo como um modelo base para o documento de registro.
Não modifique ou remova nenhum script presente no modelo base.

**Modificação do modelo base**

* Se você não estiver aplicando nenhum estilo sobre campos no template base, é aconselhável remover esses campos do template base para que todas as atualizações no template base sejam selecionadas automaticamente.
* Ao modificar o modelo base, não remova, adicione ou modifique scripts.

>[!NOTE]
>
>Modelo de base de design usando convenções e seguindo rigorosamente as etapas acima.

## Documento de configuração modelo de registro {#document-of-record-template-configuration}

Configure o documento de modelo de registro do formulário para permitir que os clientes baixem uma cópia impressa amigável do formulário enviado. Um arquivo XDP serve como o documento do modelo de registro. O documento de download de clientes de registro é formatado de acordo com o layout especificado no arquivo XDP.

Execute as seguintes etapas para configurar um documento de registro para formulários adaptáveis:

1. Na instância AEM autor, clique em **Forms > Forms e Documents.**
1. Selecione um formulário e clique em **Exibir Propriedades**.
1. Na janela Propriedades, toque em **Modelo de formulário**.
Também é possível selecionar um modelo de formulário ao criar um formulário.

   >[!NOTE]
   >
   >Na guia Modelo de formulário, selecione **Esquema** ou **Nenhum** no menu suspenso **Selecionar de**. **[!UICONTROL O documento de registro não é compatível com formulários adaptáveis ou baseados em XFA com o modelo de formulário como modelo de formulário.]**

1. Na seção Document of Record Template Configuration da guia Form Model , selecione uma das seguintes opções.

   **** NenhumSelecione esta opção se não quiser configurar o documento de registro para o formulário.

   **Associar Modelo de Formulário como Documento de** Modelo de RegistroSelecione esta opção se tiver um arquivo XDP que deseja usar como modelo para o documento de registro. Ao selecionar essa opção, todos os arquivos XDP disponíveis no repositório AEM Forms são exibidos. Selecione o arquivo apropriado.

   O arquivo XDP selecionado é associado ao formulário adaptável.

   **Gerar Documento de** RegistroSelecione esta opção para usar um arquivo XDP como modelo base para definir o estilo e a aparência do documento de registro. Ao selecionar essa opção, todos os arquivos XDP disponíveis no repositório AEM Forms são exibidos. Selecione o arquivo apropriado.

   >[!NOTE]
   >
   >Certifique-se de que o esquema usado para criar um formulário adaptável e um esquema (esquema de dados) do Formulário XFA seja o mesmo se:
   >
   >
   >
   >    * O formulário adaptável é baseado em esquema
   >    * Você está usando a opção **Associar Modelo de Formulário como o Documento de Registro Modelo** para o documento de registro


1. Clique em **Concluído.**

## Personalizar as informações da marca no documento de registro {#customize-the-branding-information-in-document-of-record}

Ao gerar um documento de registro, você pode alterar as informações de marca do documento de registro na guia Documento de registro. A guia Documento de registro inclui opções como logotipo, aparência, layout, cabeçalho e rodapé, aviso de isenção de responsabilidade e se você deseja ou não incluir as opções de caixa de seleção e botão de opção não selecionadas.

Para localizar as informações de marca inseridas na guia Document of Record , verifique se a localidade do navegador está definida adequadamente. Para personalizar as informações de marca do documento de registro, execute as seguintes etapas:

1. Selecione um painel (painel raiz) no documento de registro e toque em ![configurar](assets/configure.png).
1. Toque em ![dortab](assets/dortab.png). A guia Document of Record é exibida.
1. Selecione o modelo padrão ou um modelo personalizado para renderizar o documento de registro. Se você selecionar o modelo padrão, uma visualização em miniatura do documento de registro será exibida abaixo da lista suspensa Modelo .

   ![modelo de marca](assets/brandingtemplate.png)

   Se você optar por selecionar um modelo personalizado, navegue por um XDP selecionado no servidor do AEM Forms. Se você quiser usar um modelo que ainda não esteja no servidor do AEM Forms, primeiro carregue o XDP no servidor do AEM Forms.

1. Com base na seleção de um modelo padrão ou personalizado, algumas ou todas as propriedades a seguir serão exibidas na guia Documento de registro. Especifique estes adequadamente:

   * **Imagem** do logotipo: Você pode optar por usar a imagem do logotipo no formulário adaptável, escolher um DAM ou fazer upload de um de seu computador.
   * **Título do formulário**
   * **Texto do cabeçalho**
   * **Rótulo do aviso**
   * **Aviso**
   * **Texto do aviso**
   * **Cor** do destaque: A cor na qual o texto do cabeçalho e as linhas separadoras são renderizados no documento ou registro em PDF
   * **Família** de fontes: Família de fontes do texto no documento de registro PDF
   * **Para os componentes Caixa de seleção e Botão de opção , mostrar somente os valores selecionados**
   * **Separador para vários valores selecionados**
   * **Incluir objetos de formulário que não estão vinculados ao modelo de dados**
   * **Excluir campos ocultos do documento de registro**
   * **Ocultar descrição de painéis**

   >[!NOTE]
   >
   >Se você estiver usando um modelo de formulário adaptável criado com uma versão do Designer anterior à 6.3, para que as propriedades Cores do destaque e Família de fontes funcionem, verifique se o seguinte está presente no modelo de formulário adaptável abaixo do subformulário raiz:

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

1. Para salvar as alterações da marca, toque em Concluído.

## Layouts de tabela e coluna para painéis no Documento de registro {#table-and-column-layouts-for-panels-in-document-of-record}

O formulário adaptável pode ser longo, com vários campos de formulário. Talvez você não queira salvar um documento de registro como uma cópia exata do formulário adaptável. Agora é possível escolher um layout de tabela ou coluna para salvar um ou mais painéis de formulário adaptáveis no documento de registrar PDF.

Antes de gerar um documento de registro, nas configurações de um painel, selecione Layout para o documento de registro desse painel como Tabela ou Coluna. Os campos no painel são organizados adequadamente no documento de registro.

![Campos em um painel renderizado em um layout de tabela no documento de registro](assets/dortablelayout.png)

Campos em um painel renderizado em um layout de tabela no documento de registro

![Campos em um painel renderizado em um layout de coluna no documento de registro](assets/dorcolumnlayout.png)

Campos em um painel renderizado em um layout de coluna no documento de registro

## Configurações do documento de registro {#document-of-record-settings}

As configurações de documento de registro permitem que você escolha as opções que deseja incluir no documento de registro. Por exemplo, um banco aceita nome, idade, número de segurança social e número de telefone em um formulário. O formulário gera um número de conta bancária e detalhes da ramificação. Você pode optar por exibir somente o nome, o número da previdência social, a conta bancária e os detalhes da ramificação no documento de registro.

O documento de configurações de registro de um componente está disponível em suas propriedades. Para acessar as propriedades de um componente, selecione o componente e clique em ![cmppr](assets/cmppr.png) na sobreposição. As propriedades são listadas na barra lateral e você pode encontrar as seguintes configurações nela.

**Configurações de nível de campo**

* **Excluir do documento de registro**: A definição da propriedade true exclui o campo do documento de registro. Essa é uma propriedade capaz de script chamada `excludeFromDoR`. Seu comportamento depende de **Excluir campos do DoR se a propriedade de nível de formulário oculta**.

* **Exibir painel como tabela:** Definir a propriedade exibe o painel como tabela no documento de registro se o painel tiver menos de 6 campos. Aplicável somente para painel.
* **Excluir título do Documento de registro:** Definir a propriedade exclui o título do painel/tabela do documento de registro. Aplicável somente para painel e tabela.
* **Excluir descrição do documento de registro:** definir a propriedade exclui a descrição do painel/tabela do documento de registro. Aplicável somente para painel e tabela.

**Configurações de nível de formulário**

* **Incluir campos não vinculados no DoR:** a configuração da propriedade inclui campos não vinculados do formulário adaptável baseado em Esquema no documento de registro. Por padrão, é verdadeiro.
* **Excluir campos do DoR se ocultos:** a configuração da propriedade substitui o comportamento da propriedade de nível de campo &quot;Excluir do documento de registro&quot; quando não é verdadeira. Se os campos estiverem ocultos no momento do envio do formulário, eles serão excluídos do documento de registro se a propriedade estiver definida como true, desde que a propriedade &quot;Excluir do documento de registro&quot; não esteja definida.

## Considerações principais ao trabalhar com o documento de registro {#key-considerations-when-working-with-document-of-record}

Lembre-se das considerações e limitações a seguir ao trabalhar no documento de registro de formulários adaptáveis.

* O documento de modelos de registro não suporta Rich Text. Portanto, qualquer rich text no formulário adaptável estático ou nas informações preenchidas pelo usuário final aparece como texto sem formatação no documento de registro.
* Os fragmentos de documento em um formulário adaptável não aparecem no documento de registro. No entanto, fragmentos de formulário adaptáveis são compatíveis.
* Não há suporte para vínculo de conteúdo no documento de registro gerado para o formulário adaptável baseado no Esquema XML.
* A versão localizada do documento de registro é criada sob demanda para uma localidade quando o usuário solicita a renderização do documento de registro. A localização do documento de registro ocorre juntamente com a localização do formulário adaptável. Para obter mais informações sobre a localização do documento de formulários de registro e adaptáveis, consulte [Usar fluxo de trabalho de tradução AEM para localizar formulários adaptáveis e documentos de registro](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

