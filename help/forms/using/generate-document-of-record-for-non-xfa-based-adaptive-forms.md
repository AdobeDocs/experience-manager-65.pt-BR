---
title: Gerar documento de registro para formulários adaptáveis
description: Explica como gerar documentos de registro (DoR) para formulários adaptáveis.
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 7240897f-6b3a-427a-abc6-66310c2998f3
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '4308'
ht-degree: 2%

---

# Gerar documento de registro para formulários adaptáveis ou fragmentos de formulário adaptáveis {#generate-document-of-record-for-adaptive-forms}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=pt-br) |
| AEM 6.5 | Este artigo |


## Visão geral {#overview}

Depois de enviar um formulário, seus clientes geralmente querem manter um registro, em formato impresso ou de documento, das informações que preencheram no formulário para referência futura. Isso é chamado de documento de registro.

Este artigo explica como gerar um documento de registro para o Forms adaptável ou fragmento do Formulário adaptável.

>[!NOTE]
>
> O suporte para personalizar os fragmentos de formulário adaptável e seus campos no editor de formulário adaptável foi introduzido com o AEM 6.5 Forms Service Pack 19 (6.5.19.0).


>[!NOTE]
>
>A geração automática de documento de registro não é compatível com formulários adaptáveis baseados em XFA. No entanto, é possível usar o XDP usado para criar o formulário adaptável como documento de registro.

## Tipos de formulário adaptável e seus documentos de registro {#adaptive-form-types-and-their-documents-of-record}

Ao criar um formulário adaptável, você pode selecionar um modelo de formulário. As opções são:

* [Modelos de formulário](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
Permite selecionar um modelo XFA para o formulário adaptável. Ao selecionar um modelo XFA, você pode usar o arquivo XDP associado para o documento de registro, conforme descrito acima.

* [Esquema XML](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
Permite selecionar uma definição de esquema XML para o formulário adaptável. Ao selecionar um esquema XML para seu formulário adaptável, você pode:

   * Associe um modelo XFA para o documento de registro. Certifique-se de que o modelo XFA associado use o mesmo esquema XML que o formulário adaptável
   * Gerar automaticamente documento de registro

* Nenhum
Permite criar um formulário adaptável sem um modelo de formulário. O documento de registro é gerado automaticamente para o formulário adaptável.

Ao selecionar um modelo de formulário, configure o documento de registro usando as opções disponíveis em Documento de configuração do modelo de registro. Consulte [Documento de configuração de modelo de registro](#document-of-record-template-configuration).

## Documento de registro gerado automaticamente {#automatically-generated-document-of-record}

Um documento de registro permite que seus clientes mantenham uma cópia do formulário enviado para fins de impressão. Quando você gera automaticamente um documento de registro, sempre que você altera o formulário, o documento de registro dele é atualizado imediatamente. Por exemplo, você remove o campo de idade para clientes que selecionam Estados Unidos da América como seu país. Quando esses clientes geram um documento de registro, o campo de idade não fica visível para eles no documento de registro.

O documento de registro gerado automaticamente tem as seguintes vantagens:

* Ele cuida da vinculação de dados.
* Ele oculta automaticamente os campos marcados como excluir do documento de registro no momento do envio. Não é necessário nenhum esforço extra.
* Ele economiza tempo para projetar o documento do modelo de registro.
* Ele permite tentar diferentes estilos e aparências usando diferentes modelos base e escolher o melhor estilo e aparência para o Documento de registro. As aparências de estilo são opcionais e, se você não especificar o estilo, os estilos do sistema serão definidos como padrão.
* Garante que qualquer alteração no formulário seja refletida imediatamente no documento de registro.

## Componentes para gerar automaticamente um documento de registro {#components-to-automatically-generate-a-document-of-record}

Para gerar um documento de registro para formulários adaptáveis, você precisa dos seguintes componentes:

**Formulário adaptável** Formulário adaptável para o qual você deseja gerar um documento de registro.

**Fragmento de formulário adaptável** Fragmento de formulário adaptável para o qual você deseja gerar um documento de registro.

**Modelo base (recomendado)** Modelo XFA (arquivo XDP) criado no AEM Designer. O modelo base é usado para especificar informações de estilo e identidade visual para o documento de modelo de registro.

Consulte [Modelo base de um documento de registro](#base-template-of-a-document-of-record)

>[!NOTE]
>
>O modelo base de um documento de registro também é chamado de metamodelo de um documento de registro.

**Documento de modelo de registro** Modelo XFA (arquivo XDP) gerado de um formulário adaptável.

Consulte [Documento de configuração de modelo de registro](#document-of-record-template-configuration).

**Dados do formulário** Informações preenchidas por um usuário no formulário adaptável. Ele é mesclado com o documento do modelo de registro para gerar o documento de registro.

## Mapeamento de elementos de formulário adaptáveis {#mapping-of-adaptive-form-elements}

As seções a seguir descrevem como os elementos de formulário adaptáveis aparecem no documento de registro.

### Campos {#fields}

<table>
 <tbody>
  <tr>
   <th>Componente de formulário adaptável</th>
   <th>Componente XFA correspondente</th>
   <th>Incluído por padrão no documento de modelo de registro?</th>
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
   <td>Rabisco de assinatura</td>
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
   <td><p>Botão Enviar de email</p> <p>Botão Enviar do HTTP</p> </td>
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
   <td>Não disponível no documento de modelo de registro. Disponível somente no documento de registro por meio de anexos.</td>
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
   <td>O painel repetível é mapeado para um subformulário repetível.</td>
  </tr>
 </tbody>
</table>

### Componentes estáticos {#static-components}

| Componente de formulário adaptável | Componente XFA correspondente | Notas |
|---|---|---|
| Imagem | Imagem | Os componentes TextDraw e Image, vinculados ou não, sempre aparecem no documento de registro para um formulário adaptável baseado em XSD, a menos que sejam excluídos usando o documento de configurações de registro. |
| Texto | Texto |

>[!NOTE]
>
>Na interface clássica, você obtém diferentes guias para editar propriedades de campos.

### Tabelas {#tables}

Os componentes da tabela de formulários adaptáveis, como cabeçalho, rodapé e mapa de linhas para componentes XFA correspondentes. Você pode mapear painéis repetíveis para tabelas no documento de registro.

## Modelo base de um documento de registro {#base-template-of-a-document-of-record}

O modelo base fornece informações de estilo e aparência ao documento de registro. Ele permite personalizar a aparência padrão do documento de registro gerado automaticamente. Por exemplo, você deseja adicionar o logotipo da empresa no cabeçalho e as informações de direitos autorais no rodapé do documento de registro. A página mestra do modelo base é usada como uma página mestra do documento de modelo de registro. A página-mestre pode ter informações como cabeçalho, rodapé e número de página que podem ser aplicadas ao documento de registro. É possível aplicar essas informações ao documento de registro usando o modelo base para geração automática do documento de registro. O uso do template base permite alterar as propriedades padrão dos campos.

Siga as [Convenções do modelo base](#base-template-conventions) ao criar o modelo base.

## Convenções do modelo base {#base-template-conventions}

Um modelo base é usado para definir o cabeçalho, rodapé, estilo e aparência de um documento de registro. O cabeçalho e o rodapé podem incluir informações como o logotipo da empresa e o texto de direitos autorais. A primeira página mestra no modelo base é copiada e usada como página mestra do documento de registro, que contém o cabeçalho, o rodapé, o número da página ou qualquer outra informação que deva aparecer em todas as páginas do documento de registro. Se você estiver usando um modelo base que não esteja em conformidade com as convenções do modelo base, a primeira página mestra do modelo base ainda será usada no documento de modelo de registro. É altamente recomendável que você crie seu modelo base de acordo com suas convenções e o use para a geração automática do documento de registro.

**Convenções de página mestra**

* No modelo base, você deve nomear o subformulário raiz como `AF_METATEMPLATE` e a página mestra como `AF_MASTERPAGE`.

* A página mestra com o nome `AF_MASTERPAGE`, localizada no subformulário raiz `AF_METATEMPLATE`, recebe preferência para extrair informações de cabeçalho, rodapé e estilo.

* Se `AF_MASTERPAGE` estiver ausente, a primeira página mestra presente no modelo base será usada.

**Convenções de estilo para campos**

* Para aplicar estilo aos campos no documento de registro, o modelo base fornece campos no subformulário `AF_FIELDSSUBFORM` sob o subformulário raiz `AF_METATEMPLATE`.

* As propriedades desses campos são aplicadas aos campos no documento de registro. Esses campos devem seguir a convenção de nomenclatura `AF_<name of field in all caps>_XFO`. Por exemplo, o nome do campo da caixa de seleção deve ser `AF_CHECKBOX_XFO`.

Para criar um template base, faça o seguinte no AEM Designer.

1. Clique em **Arquivo > Novo**.
1. Selecione a opção **Baseado em um modelo**.

1. Selecione a categoria **Forms - Documento de Registro**.
1. Selecione **Modelo Base DoR**.
1. Clique em **Avançar** e forneça as informações necessárias.

1. (Opcional) Modifique o estilo e a aparência dos campos que deseja aplicar nos campos do documento de registro.
1. Salve o formulário.

Agora você pode usar o formulário salvo como um modelo base para o documento de registro.
Não modifique ou remova scripts presentes no modelo base.

**Modificando modelo base**

* Se você não estiver aplicando nenhum estilo sobre os campos no modelo base, é aconselhável remover esses campos do modelo base para que todas as atualizações do modelo base sejam selecionadas automaticamente.
* Ao modificar o modelo base, não remova, adicione ou modifique scripts.

>[!NOTE]
>
>Modelo de base de design usando convenções e seguindo estritamente as etapas acima.

## Documento de configuração modelo de registro {#document-of-record-template-configuration}

Configure o documento de modelo de registro do seu formulário para permitir que os clientes baixem uma cópia impressa do formulário enviado. Um arquivo XDP serve como o documento do modelo de registro. O documento de download dos clientes do registro é formatado de acordo com o layout especificado no arquivo XDP.

Execute as seguintes etapas para configurar um documento de registro para formulários adaptáveis:

1. Na instância do autor AEM, clique em **Forms > Forms e Documentos.**
1. Selecione um formulário e clique em **Exibir Propriedades**.
1. Na janela Propriedades, selecione **Modelo de formulário**.
Você também pode selecionar um modelo de formulário ao criar um formulário.

   >[!NOTE]
   >
   >Na guia Modelo de formulário, selecione **Esquema** ou **Nenhum** no menu suspenso **Selecionar de**. **[!UICONTROL Não há suporte para o documento de registro em formulários baseados em XFA ou adaptáveis com o Modelo de formulário como modelo de formulário.]**

1. Na seção Document of Record Template Configuration da guia Form Model, selecione uma das seguintes opções:

   **Nenhum** Selecione esta opção se não quiser configurar o documento de registro para o formulário.

   **Associar modelo de formulário como documento de modelo de registro** Selecione esta opção se você tiver um arquivo XDP que deseja usar como modelo para o documento de registro. Ao selecionar essa opção, todos os arquivos XDP disponíveis no repositório do AEM Forms são exibidos. Selecione o arquivo apropriado.

   O arquivo XDP selecionado é associado ao formulário adaptável.

   **Gerar documento de registro** Selecione esta opção para usar um arquivo XDP como modelo base para definir o estilo e a aparência do documento de registro. Ao selecionar essa opção, todos os arquivos XDP disponíveis no repositório do AEM Forms são exibidos. Selecione o arquivo apropriado.

   >[!NOTE]
   >
   >Verifique se o esquema usado para criar o formulário adaptável e o esquema (esquema de dados) do Formulário XFA são iguais se:
   >
   >
   >
   >    * Seu formulário adaptável é baseado em esquema
   >    * Você está usando a opção **Associar Modelo de Formulário como Documento de Modelo de Registro** para o documento de registro
   >
   >

1. Clique em **Concluído.**

## Personalizar as informações de marca no documento de registro {#customize-the-branding-information-in-document-of-record}

Ao gerar um documento de registro, você pode alterar as informações de marca do documento de registro na guia Documento de registro. A guia Documento de registro inclui opções como logotipo, aparência, layout, cabeçalho e rodapé, aviso de isenção e se você deseja ou não incluir opções de caixa de seleção e botão de opção não selecionados.

Para localizar as informações de marca inseridas na guia Documento de registro, é necessário garantir que o local do navegador esteja definido adequadamente. Para personalizar as informações de marca do documento de registro, conclua as seguintes etapas:

1. Selecione um painel (painel raiz) no documento de registro e selecione ![configurar](assets/configure.png).
1. Selecione ![dortab](/help/forms/using/assets/dortab.png). A guia Documento de registro é exibida.
1. Selecione o modelo padrão ou um modelo personalizado para renderizar o documento de registro. Se você selecionar o modelo padrão, uma visualização em miniatura do documento de registro será exibida abaixo do menu suspenso Modelo.

   ![modelo de marca](/help/forms/using/assets/brandingtemplateupdate.png)

   Se você optar por selecionar um modelo personalizado, procure e selecione um XDP no servidor do AEM Forms. Se quiser usar um modelo que ainda não esteja no servidor do AEM Forms, primeiro faça upload do XDP para o seu servidor do AEM Forms.

### Propriedades da página principal (#master-page-properties)

Se você selecionar um modelo padrão ou personalizado, algumas ou todas as propriedades de página-mestre a seguir serão exibidas na guia Documento de registro, como mostrado na imagem acima. Especifique esses itens adequadamente:

* **Imagem de logotipo**: você pode optar por usar a imagem de logotipo do formulário adaptável, escolher uma do DAM ou carregar uma do seu computador.
* **Título do formulário**
* **Texto do Cabeçalho**
* **Rótulo do aviso**
* **Aviso de isenção de responsabilidade**
* **Texto do aviso**

  <!--
    * **Accent Color**: The color in which header text and separator lines are rendered in the document or record PDF
    * **Font Family**: Font family of the text in the document of record PDF
    * **For Check Box and Radio Button components, show only the selected values**
    * **Separator for multiple selected value(s)**
    * **Include form objects that are not bound to data model**
    * **Exclude hidden fields from the document of record**
    * **Hide description of panels**
    -->

  Se o modelo XDP personalizado selecionado incluir várias páginas mestras, as propriedades dessas páginas aparecerão na seção **[!UICONTROL conteúdo]** da guia **[!UICONTROL Documento de Registro]**.

  ![Propriedades da Página Mestra](assets/master-page-properties.png)

  As propriedades da página principal incluem Imagem de logotipo, Texto do cabeçalho, Título do formulário, Rótulo do aviso e Texto do aviso. Você pode aplicar propriedades de formulário adaptável ou modelo XDP ao documento de registro. Por padrão, o AEM Forms aplica as propriedades do modelo ao Documento de registro. Você também pode definir valores personalizados para as propriedades da página-mestre. Para obter informações sobre como aplicar várias páginas mestras em um Documento de Registro, consulte [Aplicar várias páginas mestras a um Documento de Registro](#apply-multiple-master-pages-dor).

  >[!NOTE]
  >
  >Se você estiver usando um modelo de formulário adaptável criado com uma versão do Designer anterior à 6.3, para que as propriedades de Cor de ênfase e Família de fontes funcionem, verifique se o seguinte está presente no modelo de formulário adaptável no subformulário raiz:

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

1. Para salvar as alterações de marca, selecione Concluído.

## Layouts de tabela e coluna para painéis no documento de registro {#table-and-column-layouts-for-panels-in-document-of-record}

O formulário adaptável pode ser longo, com vários campos de formulário. Talvez você não queira salvar um documento de registro como uma cópia exata do formulário adaptável. Agora é possível escolher um layout de tabela ou coluna para salvar um ou mais painéis de formulário adaptáveis no documento de PDF de registro.

Antes de gerar um documento de registro, nas configurações de um painel, selecione Layout do documento de registro desse painel como Tabela ou Coluna. Os campos no painel são organizados de acordo no documento de registro.

![Campos em um painel renderizados em um layout de tabela no documento de registro](assets/dortablelayout.png)

Campos em um painel renderizado em um layout de tabela no documento de registro

![Campos em um painel renderizados em um layout de coluna no documento de registro](assets/dorcolumnlayout.png)

Campos em um painel renderizado em um layout de coluna no documento de registro

## Configurações do documento de registro {#document-of-record-settings}

As configurações de documento de registro permitem escolher as opções que deseja incluir no documento de registro. Por exemplo, um banco aceita nome, idade, número de seguridade social e número de telefone em um formulário. O formulário gera um número de conta bancária e detalhes da agência. Você pode optar por exibir somente o nome, o número de seguridade social, a conta bancária e os detalhes da agência no documento de registro.

O documento de configurações de registro de um componente está disponível em suas propriedades. Para acessar as propriedades de um componente, selecione o componente e clique em ![cmppr](assets/cmppr.png) na sobreposição. As propriedades são listadas na barra lateral e você pode encontrar as seguintes configurações.

**Configurações de nível de campo**

* **Excluir do documento de registro**: definir a propriedade true exclui o campo do documento de registro. Esta é uma propriedade que pode ser gerada por script chamada `excludeFromDoR`. Seu comportamento depende de **Excluir campos do DoR se ocultos** propriedade de nível de formulário.

* **Exibir painel como tabela:** Definir a propriedade exibe o painel como tabela no documento de registro se o painel tiver menos de 6 campos. Aplicável somente para o painel.
* **Excluir título do documento de registro:** a configuração da propriedade exclui título do painel/tabela do documento de registro. Aplicável somente para painel e tabela.
* **Excluir descrição do documento de registro:** a configuração da propriedade exclui a descrição do painel/tabela do documento de registro. Aplicável somente para painel e tabela.
* **[!UICONTROL Paginação]** > **[!UICONTROL Local]**: determina onde você seleciona posicionar o painel.
   * **[!UICONTROL Colocar]** > **[!UICONTROL Seguinte Anterior]**: coloca o painel depois do objeto anterior no painel pai.
   * **[!UICONTROL Colocar]** > **[!UICONTROL Na área de conteúdo]** > Nome da área de conteúdo: coloca o painel na área de conteúdo especificada.
   * **[!UICONTROL Inserir]** > **[!UICONTROL Início da Próxima Área de Conteúdo]**: coloca o painel na parte superior da próxima área de conteúdo.
   * **[!UICONTROL Local]** > **[!UICONTROL Início da Área de Conteúdo]** > Nome da área de conteúdo: coloca o painel na parte superior da área de conteúdo especificada.
   * **[!UICONTROL Colocar]** > **[!UICONTROL Na página]** > Nome da página mestra: coloca o painel na página especificada. Se uma quebra de página não for inserida automaticamente, [!DNL AEM Forms] adicionará uma quebra de página.
   * **[!UICONTROL Inserir]** > **[!UICONTROL Início da Próxima Página]**: coloca o painel no topo da próxima página. Se uma quebra de página não for inserida automaticamente, [!DNL AEM Forms] adicionará uma quebra de página.
   * **[!UICONTROL Local]** > **[!UICONTROL Início da Página]** > Nome da página mestra: coloca o painel na parte superior da página quando a página especificada é renderizada. Se uma quebra de página não for inserida automaticamente, [!DNL AEM Forms] adicionará uma quebra de página.
* **[!UICONTROL Paginação]** > **[!UICONTROL Depois]**: determina qual área deve ser preenchida depois que um painel é colocado. Os seguintes campos estão disponíveis na seção **[!UICONTROL Depois]**:
   * **[!UICONTROL Depois]** > **[!UICONTROL Continuar Preenchendo Pai]**: continua mesclando dados para todos os objetos restantes a serem preenchidos no painel pai.
   * **[!UICONTROL Depois]** > **[!UICONTROL Ir para a próxima área de conteúdo]**: começa a preencher a próxima área de conteúdo depois de posicionar o painel.
   * **[!UICONTROL Depois]** > **[!UICONTROL Ir para a área de conteúdo]** > Nome da área de conteúdo: começa a preencher a área de conteúdo especificada após posicionar o painel.
   * **[!UICONTROL Depois]** > **[!UICONTROL Ir para a Próxima Página]**: começa a preencher a próxima página após posicionar o painel.
   * **[!UICONTROL Depois]** > **[!UICONTROL Ir para Página]** > Nome da página: começa a preencher a página especificada após posicionar o painel.
* **[!UICONTROL Paginação]** > **[!UICONTROL Estouro]**: define um estouro para um painel ou uma tabela que abrange páginas. Os seguintes campos estão disponíveis na seção **[!UICONTROL Estouro]**:
   * **[!UICONTROL Estouro]** > **[!UICONTROL Nenhum]**: começa a preencher a próxima página. Se uma quebra de página não for inserida automaticamente, [!DNL AEM Forms] adicionará uma quebra de página.
   * **[!UICONTROL Estouro]** > **[!UICONTROL Ir para a Área de Conteúdo]** > Nome da área de conteúdo: começa a preencher a área de conteúdo especificada.
   * **[!UICONTROL Estouro]** > **[!UICONTROL Ir para Página]** > Nome da página: inicia o preenchimento da página especificada.

  >[!NOTE]
  >
  > A propriedade de paginação não está disponível para fragmentos de formulário adaptáveis.

Para obter informações sobre como aplicar quebras de página e aplicar várias páginas mestras em um Documento de Registro, consulte [Aplicar quebra de página em um Documento de Registro](#apply-page-breaks-in-dor) e [Aplicar várias páginas mestras a um Documento de Registro](#apply-multiple-master-pages-dor).

**Configurações de nível de formulário**

* **[!UICONTROL BÁSICO]**
   * **Modelo:** Você pode selecionar o modelo Padrão ou Personalizado.

     ![alt texto](image.png)
   * **Cor de Ênfase:** Você pode predefinir a Cor do modelo do [!UICONTROL Documento de Registro].
   * **Família da Fonte:** Selecione o tipo de fonte para os textos do [!UICONTROL Documento de Registro].
   * **Incluir campos não associados em DoR:** A configuração da propriedade inclui campos não associados do formulário adaptável baseado em esquema no [!UICONTROL Documento de Registro]. Por padrão, é verdadeiro.
   * **Excluir campos do DoR se ocultos:** Defina a propriedade para excluir os campos ocultos do [!UICONTROL Documento de Registro] no envio do formulário. Ao habilitar [Revalidar no servidor](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form), o servidor recalcula os campos ocultos antes de excluir esses campos do [!UICONTROL Documento de Registro]
* **[!UICONTROL PROPRIEDADES DO CAMPO DE FORMULÁRIO]**
   * Se você marcar a opção **Para os componentes Caixa de Seleção e Botão de Opção, mostrar somente os valores selecionados**, ela gerará a saída do DoR somente com os valores selecionados.
   * Você pode selecionar Separador para vários valores selecionados ou escolher qualquer outro tipo de separador.
   * Alinhamento de opções
      * Vertical
      * Horizontal
      * O mesmo que o formulário adaptável

     >[!NOTE]
     > O alinhamento vertical e horizontal é aplicável apenas a     Botão de opção e caixa de seleção
* **[!UICONTROL PROPRIEDADES DA PÁGINA MESTRA]** Clique para obter mais informações sobre [propriedades da Página Mestra](#master-page-properties-master-page-properties)

## Aplicar uma quebra de página em um documento de registro {#apply-page-breaks-in-dor}

Você pode aplicar quebras de página em um Documento de registro usando vários métodos.

Para aplicar uma quebra de página a um documento de registro:

1. Selecione o painel e selecione ![Configurar](/help/forms/using/assets/configure.png)
1. Expanda **[!UICONTROL Documento de Registro]** para exibir as propriedades.

1. Na seção **[!UICONTROL Paginação]**, selecione ![Pasta](/help/forms/using/assets/folder-icon.png) no campo **[!UICONTROL Local]**.
1. Selecione **[!UICONTROL Início da Próxima página]** e selecione **[!UICONTROL Selecionar]**. Você também pode selecionar **[!UICONTROL Início da página]**, selecionar a página mestra e **[!UICONTROL Selecionar]** para aplicar a quebra de página.
1. Selecione ![Salvar](/help/forms/using/assets/save_icon.png) para salvar as propriedades.

O painel selecionado é movido para a próxima página.

## Aplicar várias páginas-mestre a um documento de registro {#apply-multiple-master-pages-dor}

Se o modelo XDP personalizado selecionado incluir várias páginas mestras, as propriedades dessas páginas aparecerão na seção [!UICONTROL conteúdo] da guia [!UICONTROL Documento de Registro]. Para obter mais informações, consulte [Personalizar as informações de marca no documento de registro](#customize-the-branding-information-in-document-of-record).

Você pode aplicar várias páginas-mestre a um documento de registro aplicando páginas-mestre diferentes aos componentes de um formulário adaptável. Use a seção [Paginação](#document-of-record-settings) do documento de propriedades de registro para aplicar várias páginas mestras.

Este é um exemplo de como aplicar várias páginas-mestre a um documento de registro:
Você carrega um modelo XDP que inclui quatro páginas mestras no servidor [!DNL AEM Forms]. [!DNL AEM Forms] aplica as propriedades do modelo ao Documento de Registro por padrão. [!DNL AEM Forms] também aplica as propriedades da primeira página mestra no modelo ao documento de registro.

Para aplicar as propriedades da segunda página-mestre a um painel e as propriedades da terceira página-mestre aos painéis seguintes, execute as seguintes etapas:

1. Selecione o painel para aplicar a segunda página mestra e selecione ![Configurar](assets/cmppr.png).
1. Na seção **[!UICONTROL Paginação]**, selecione ![Pasta](/help/forms/using/assets/folder-icon.png) no campo **[!UICONTROL Local]**.
1. Selecione **[!UICONTROL Na página]**, selecione a segunda página mestra e selecione **[!UICONTROL Selecionar]**.
O AEM Forms aplica a segunda página-mestre ao painel e a todos os painéis subsequentes no formulário adaptável.
1. Na seção **[!UICONTROL Paginação]**, selecione ![Pasta](/help/forms/using/assets/folder-icon.png) no campo **[!UICONTROL Depois]**.
1. Selecione **[!UICONTROL Ir para página]**, selecione a terceira página mestra e selecione **[!UICONTROL Selecionar]**.
1. Selecione ![Salvar](/help/forms/using/assets/save_icon.png) para salvar as propriedades.
O AEM Forms aplica a terceira página-mestre ao painel e a todos os painéis subsequentes no formulário adaptável.

>[!NOTE]
>
> Não é possível aplicar várias páginas-mestre a um documento de registro para um fragmento de formulário adaptável.

## Considerações principais ao trabalhar com documento de registro {#key-considerations-when-working-with-document-of-record}

Lembre-se das seguintes considerações e limitações ao trabalhar em um documento de registro para formulários adaptáveis.

* Os modelos de documento de registro não dão suporte a rich text. Portanto, qualquer rich text no formulário adaptável estático ou nas informações preenchidas pelo usuário final aparece como texto simples no documento de registro.
* Fragmentos de documento em um formulário adaptável não aparecem no documento de registro. No entanto, os fragmentos de formulário adaptáveis são compatíveis.
* Não há suporte para a associação de conteúdo no documento de registro gerado para o formulário adaptável baseado em esquema XML.
* A versão localizada do documento de registro é criada sob demanda para um local quando o usuário solicita a renderização do documento de registro. A localização do documento de registro ocorre juntamente com a localização do formulário adaptável. Para obter mais informações sobre a localização do documento de registro e formulários adaptáveis, consulte [Usar o fluxo de trabalho de tradução do AEM para localizar formulários adaptáveis e documento de registro](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

## Usar um arquivo XCI personalizado

Um arquivo XCI ajuda a definir várias propriedades de um documento. <!-- Forms as a Cloud Service has a master XCI file.--> Você pode usar um arquivo XCI personalizado para substituir uma ou mais propriedades padrão especificadas no arquivo XCI existente. Por exemplo, você pode optar por incorporar uma fonte em um documento ou ativar a propriedade marcada para todos os documentos. A tabela a seguir especifica as opções de XCI:

| Opção XCI | Descrição |
|--- |--- |
| config/present/pdf/creator | Identifica o criador do documento usando a entrada Criador no dicionário de Informações do Documento. Para obter informações sobre este dicionário, consulte o [guia de Referência de PDF](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/). |
| config/present/pdf/producer | Identifica o produtor do documento usando a entrada Produtor no dicionário de Informações do documento. Para obter informações sobre este dicionário, consulte o [guia de Referência de PDF](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/). |
| config/present/layout | Controla se a saída é um painel único ou paginada. |
| config/present/pdf/compression/level | Especifica o grau de compactação a ser usado ao gerar um documento PDF. |
| config/present/pdf/fontInfo/embed | Controla a incorporação de fontes no documento de saída. |
| config/present/pdf/scriptModel | Controla se informações específicas de XFA são incluídas no documento PDF de saída. |
| config/present/common/data/adjustData | Controla se o aplicativo XFA ajusta os dados após a mesclagem. |
| config/present/pdf/renderPolicy | Controla se a geração do conteúdo da página é feita no servidor ou adiada para o cliente. |
| configuração/presente/comum/local | Especifica a localidade padrão usada no documento de saída. |
| config/present/destination | Quando contido por um elemento presente, especifica o formato de saída. Quando contido por um elemento openAction, especifica a ação a ser executada ao abrir o documento em um cliente interativo. |
| config/present/output/type | Especifica o tipo de compactação a ser aplicado a um arquivo ou o tipo de saída a ser produzido. |
| config/present/common/temp/uri | Especifica o URI do formulário. |
| config/present/common/template/base | Fornece um local base para URIs no design do formulário. Quando este elemento estiver ausente ou vazio, o local do design do formulário será usado como base. |
| config/present/common/log/to | Controla o local onde os dados de log ou de saída são gravados. |
| config/present/output/to | Controla o local onde os dados de log ou de saída são gravados. |
| config/present/script/currentPage | Especifica a página inicial quando o documento é aberto. |
| config/present/script/exclude | Informa o Forms as a Cloud Service sobre quais eventos ignorar. |
| config/present/pdf/linearized | Controla se o documento de PDF de saída está linearizado. |
| config/present/script/runScripts | Controla qual conjunto de scripts o Forms as a Cloud Service executa. |
| config/present/pdf/tagged | Controla a inclusão de tags no documento de PDF de saída. As tags, no contexto de PDF, são informações adicionais incluídas em um documento para expor a estrutura lógica do documento. As tags auxiliam na acessibilidade e na reformatação. Por exemplo, um número de página pode ser marcado como um artefato para que um leitor de tela não o enuncie no meio do texto. Embora as tags tornem um documento mais útil, elas também aumentam o tamanho do documento e o tempo de processamento para criá-lo. |
| config/present/pdf/fontInfo/alwaysEmbed | Especifica uma fonte que está incorporada no documento de saída. |
| config/present/pdf/fontInfo/neverEmbed | Especifica uma fonte que nunca deve ser incorporada ao documento de saída. |
| config/present/pdf/pdfa/part | Especifica o número da versão da especificação de PDF/A com a qual o documento está em conformidade. |
| config/present/pdf/pdfa/amd | Especifica o nível de alteração da especificação PDF/A. |
| config/present/pdf/pdfa/conformance | Especifica o nível de conformidade com a especificação PDF/A. |
| config/present/pdf/version | Especifica a versão do documento PDF a ser gerada |
| config/present/pdf/version/map | Especifica as fontes de fallback do documento |


<!--

### Use a custom XCI file in your AEM Forms environment

  1. Add the custom XCI file to your development project.
  1. Specify the following inline property:(/help/implementing/deploying/configuring-osgi.md)
  1. Deploy the project to your AEM Forms environment. <!--Cloud Service environment
  
-->

### Usar um arquivo XCI personalizado no ambiente de desenvolvimento do Forms local

1. Carregue o arquivo XCI no ambiente de desenvolvimento local.
1. Abra o gerenciador de configurações <!--Cloud Service SDK-->. <!--The default URL is: <http://localhost:4502/system/console/configMgr>.-->
1. Localize e abra a configuração **[!UICONTROL Forms adaptável e Canal da Web de comunicação interativa]**.
1. Especifique o caminho do arquivo XCI e clique em **[!UICONTROL Salvar]**.
