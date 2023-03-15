---
title: Gerar documento de registro para formulários adaptáveis
seo-title: Generate Document of Record for adaptive forms
description: Explica como você pode gerar um modelo para um documento de registro (DoR) para formulários adaptáveis.
seo-description: Explains how you can generate a template for a document of record (DoR) for adaptive forms.
uuid: 2dc7e0de-fff9-43fa-9426-e9b047eb2595
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ce65cb5f-94ec-4423-9fa9-d617e9703091
docset: aem65
feature: Adaptive Forms
exl-id: 7240897f-6b3a-427a-abc6-66310c2998f3
source-git-commit: 85189a4c35d1409690cbb93946369244e8848340
workflow-type: tm+mt
source-wordcount: '3466'
ht-degree: 3%

---

# Gerar documento de registro para formulários adaptáveis{#generate-document-of-record-for-adaptive-forms}

## Visão geral {#overview}

Depois de enviar um formulário, os clientes geralmente desejam manter um registro, em formato impresso ou de documento, das informações que preencheram no formulário para referência futura. Isso é chamado de documento de registro.

Este artigo explica como gerar um documento de registro para formulários adaptáveis.

>[!NOTE]
>
>A geração automática de documento de registro não é compatível com formulários adaptáveis baseados em XFA. No entanto, você pode usar o XDP usado para criar o formulário adaptável como documento de registro.

## Tipos de formulário adaptável e seus documentos de registro {#adaptive-form-types-and-their-documents-of-record}

Ao criar um formulário adaptável, é possível selecionar um modelo de formulário. As opções são:

* [Modelos de formulário](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
Permite selecionar um modelo XFA para o formulário adaptável. Ao selecionar um modelo XFA, você pode usar o arquivo XDP associado para o documento de registro, conforme descrito acima.

* [Esquema XML](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
Permite selecionar uma definição de esquema XML para o formulário adaptável. Ao selecionar um esquema XML para o formulário adaptável, é possível:

   * Associe um modelo XFA para o documento de registro. Certifique-se de que o modelo XFA associado use o mesmo esquema XML que seu formulário adaptável
   * Gerar automaticamente documento de registro

* Nenhum Permite criar um formulário adaptável sem um modelo de formulário. O documento de registro é gerado automaticamente para o formulário adaptável.

Ao selecionar um modelo de formulário, configure o documento de registro usando as opções disponíveis em Document of Record Template Configuration. Consulte [Documento de configuração do modelo de registro](#document-of-record-template-configuration).

## Documento de registro gerado automaticamente {#automatically-generated-document-of-record}

Um documento de registro permite que seus clientes mantenham uma cópia do formulário enviado para fins de impressão. Quando um documento de registro é gerado automaticamente, sempre que você altera o formulário, o documento de registro é atualizado imediatamente. Por exemplo, você remove o campo de idade dos clientes que selecionam os Estados Unidos da América como seu país. Quando esses clientes geram um documento de registro, o campo idade não é visível para eles no documento de registro.

O documento de registro gerado automaticamente tem as seguintes vantagens:

* Ela cuida do vínculo de dados.
* Ele oculta automaticamente os campos marcados como excluídos do documento de registro no momento do envio. Não é necessário qualquer esforço adicional.
* Ele economiza tempo para projetar o documento do modelo de registro.
* Ele permite que você experimente diferentes estilos e aparência usando diferentes modelos base e escolha o melhor estilo e aparência para o Documento de registro. As aparências de estilo são opcionais e, se você não especificar o estilo, os estilos do sistema serão definidos como padrão.
* Garante que qualquer alteração no formulário seja refletida imediatamente no documento de registro.

## Componentes para gerar automaticamente um documento de registro {#components-to-automatically-generate-a-document-of-record}

Para gerar um documento de registro para formulários adaptáveis, você precisa dos seguintes componentes:

**Formulário adaptável** Formulário adaptável para o qual você deseja gerar um documento de registro.

**Modelo base (recomendado)** Modelo XFA (arquivo XDP) criado no AEM Designer. O modelo base é usado para especificar informações de estilo e identidade visual para o documento de modelo de registro.

Consulte [Modelo base de um documento de registro](#base-template-of-a-document-of-record)

>[!NOTE]
>
>O modelo base de um documento de registro também é chamado de metamodelo de um documento de registro.

**Documento do modelo de registro** Modelo XFA (arquivo XDP) gerado a partir de um formulário adaptável.

Consulte [Documento de configuração do modelo de registro](#document-of-record-template-configuration).

**Dados do formulário** Informações preenchidas por um usuário no formulário adaptável. Ele se mescla com o documento do template de registro para gerar o documento de registro.

## Mapeamento de elementos de formulário adaptáveis {#mapping-of-adaptive-form-elements}

As seções a seguir descrevem como os elementos de formulário adaptáveis aparecem no documento de registro.

### Campos {#fields}

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

Siga [Convenções de modelo básico](#base-template-conventions) ao criar o modelo base.

## Convenções de modelo básico {#base-template-conventions}

Um modelo base é usado para definir o cabeçalho, o rodapé, o estilo e a aparência de um documento de registro. O cabeçalho e o rodapé podem incluir informações como o logotipo da empresa e o texto de direitos autorais. A primeira página principal no modelo base é copiada e usada como uma página principal para o documento de registro, que contém cabeçalho, rodapé, número de página ou qualquer outra informação que deve aparecer em todas as páginas no documento de registro. Se você estiver usando um modelo base que não está em conformidade com as convenções do modelo base, a primeira página principal do modelo base ainda será usada no documento de modelo de registro. É altamente recomendável criar seu modelo base de acordo com suas convenções e usá-lo para a geração automática de documento de registro.

**Convenções de página principais**

* No modelo base, você deve nomear o subformulário raiz como `AF_METATEMPLATE` e a página principal como `AF_MASTERPAGE`.

* A página principal com o nome `AF_MASTERPAGE` localizada na `AF_METATEMPLATE` o subformulário raiz tem preferência por extrair informações de cabeçalho, rodapé e estilo.

* If `AF_MASTERPAGE` estiver ausente, a primeira página principal presente no template base será usada.

**Convenções de estilo para campos**

* Para aplicar estilo aos campos no documento de registro, o modelo base fornece campos localizados na variável `AF_FIELDSSUBFORM` subformulário do `AF_METATEMPLATE` subformulário raiz.

* As propriedades desses campos são aplicadas aos campos no documento de registro. Esses campos devem seguir o `AF_<name of field in all caps>_XFO` convenção de nomenclatura. Por exemplo, o nome do campo para a caixa de seleção deve ser `AF_CHECKBOX_XFO`.

Para criar um modelo base, faça o seguinte no AEM Designer.

1. Clique em **Arquivo > Novo**.
1. Selecione o **Baseado em um modelo** opção.

1. Selecione o **Forms - Documento de registro** categoria .
1. Selecionar **Modelo Base DoR**.
1. Clique em **Próximo** e fornecer as informações necessárias.

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

1. Em AEM instância do autor, clique em **Forms > Forms e documentos.**
1. Selecione um formulário e clique em **Propriedades da exibição**.
1. Na janela Propriedades, toque em **Modelo de formulário**.
Também é possível selecionar um modelo de formulário ao criar um formulário.

   >[!NOTE]
   >
   >Na guia Modelo de formulário , selecione **Esquema** ou **Nenhum** do **Selecionar de** lista suspensa. **[!UICONTROL O documento de registro não é compatível com formulários adaptáveis ou baseados em XFA com o modelo de formulário como modelo de formulário.]**

1. Na seção Document of Record Template Configuration da guia Form Model , selecione uma das seguintes opções.

   **Nenhum** Selecione essa opção se não quiser configurar o documento de registro para o formulário.

   **Associar Modelo de Formulário como Documento de Modelo de Registro** Selecione esta opção se tiver um arquivo XDP que deseja usar como modelo para o documento de registro. Ao selecionar essa opção, todos os arquivos XDP disponíveis no repositório AEM Forms são exibidos. Selecione o arquivo apropriado.

   O arquivo XDP selecionado é associado ao formulário adaptável.

   **Gerar Documento de Registro** Selecione essa opção para usar um arquivo XDP como modelo base para definir o estilo e a aparência do documento de registro. Ao selecionar essa opção, todos os arquivos XDP disponíveis no repositório AEM Forms são exibidos. Selecione o arquivo apropriado.

   >[!NOTE]
   >
   >Certifique-se de que o esquema usado para criar um formulário adaptável e um esquema (esquema de dados) do Formulário XFA seja o mesmo se:
   >
   >
   >
   >    * O formulário adaptável é baseado em esquema
   >    * Você está usando **Associar Modelo de Formulário como Documento de Modelo de Registro** opção para documento de registro


1. Clique em **Feito.**

## Personalizar as informações da marca no documento de registro {#customize-the-branding-information-in-document-of-record}

Ao gerar um documento de registro, você pode alterar as informações de marca do documento de registro na guia Documento de registro. A guia Documento de registro inclui opções como logotipo, aparência, layout, cabeçalho e rodapé, aviso de isenção de responsabilidade e se você deseja ou não incluir as opções de caixa de seleção e botão de opção não selecionadas.

Para localizar as informações de marca inseridas na guia Document of Record , verifique se a localidade do navegador está definida adequadamente. Para personalizar as informações de marca do documento de registro, execute as seguintes etapas:

1. Selecione um painel (painel raiz) no documento de registro e toque em ![configure](assets/configure.png).
1. Toque ![dortab](/help/forms/using/assets/dortab.png). A guia Document of Record é exibida.
1. Selecione o modelo padrão ou um modelo personalizado para renderizar o documento de registro. Se você selecionar o modelo padrão, uma visualização em miniatura do documento de registro será exibida abaixo da lista suspensa Modelo .

   ![modelo de marca](/help/forms/using/assets/brandingtemplate.png)

   Se você optar por selecionar um modelo personalizado, navegue por um XDP selecionado no servidor do AEM Forms. Se você quiser usar um modelo que ainda não esteja no servidor do AEM Forms, primeiro carregue o XDP no servidor do AEM Forms.

1. Com base na seleção de um modelo padrão ou personalizado, algumas ou todas as propriedades a seguir serão exibidas na guia Documento de registro. Especifique estes adequadamente:

   * **Imagem do logotipo**: Você pode optar por usar a imagem do logotipo no formulário adaptável, escolher uma no DAM ou fazer o upload de uma no seu computador.
   * **Título do formulário**
   * **Texto do cabeçalho**
   * **Rótulo do aviso**
   * **Aviso**
   * **Texto do aviso**
   * **Cor do destaque**: A cor na qual o texto do cabeçalho e as linhas separadoras são renderizados no PDF de documento ou registro
   * **Família de fontes**: Família de fontes do texto no documento de PDF de registro
   * **Para os componentes Caixa de seleção e Botão de opção , mostrar somente os valores selecionados**
   * **Separador para vários valores selecionados**
   * **Incluir objetos de formulário que não estão vinculados ao modelo de dados**
   * **Excluir campos ocultos do documento de registro**
   * **Ocultar descrição de painéis**

   Se o modelo XDP personalizado selecionado incluir várias páginas principais, as propriedades dessas páginas aparecerão na variável **[!UICONTROL conteúdo]** da seção **[!UICONTROL Documento de registro]** guia .

   ![Página principal  Propriedades](assets/master-page-properties.png)

   As propriedades principais da página incluem Imagem do logotipo, Texto do cabeçalho, Título do formulário, Rótulo do aviso e Texto de isenção de responsabilidade. Você pode aplicar propriedades de formulário adaptável ou de modelo XDP ao Documento de registro. Por padrão, o AEM Forms aplica as propriedades do modelo ao Documento de registro. Também é possível definir valores personalizados para as propriedades principais da página. Para obter informações sobre como aplicar várias páginas principais em um Documento de registro, consulte [Aplicar várias páginas principais a um documento de registro](#apply-multiple-master-pages-dor).

   >[!NOTE]
   >
   >Se você estiver usando um modelo de formulário adaptável criado com uma versão do Designer anterior à 6.3, para que as propriedades Cores do destaque e Família de fontes funcionem, verifique se o seguinte está presente no modelo de formulário adaptável sob o subformulário raiz:

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

O formulário adaptável pode ser longo, com vários campos de formulário. Talvez você não queira salvar um documento de registro como uma cópia exata do formulário adaptável. Agora é possível escolher um layout de tabela ou coluna para salvar um ou mais painéis de formulário adaptáveis no documento do PDF de registro.

Antes de gerar um documento de registro, nas configurações de um painel, selecione Layout para o documento de registro desse painel como Tabela ou Coluna. Os campos no painel são organizados adequadamente no documento de registro.

![Campos em um painel renderizado em um layout de tabela no documento de registro](assets/dortablelayout.png)

Campos em um painel renderizado em um layout de tabela no documento de registro

![Campos em um painel renderizado em um layout de coluna no documento de registro](assets/dorcolumnlayout.png)

Campos em um painel renderizado em um layout de coluna no documento de registro

## Configurações do documento de registro {#document-of-record-settings}

As configurações de documento de registro permitem que você escolha as opções que deseja incluir no documento de registro. Por exemplo, um banco aceita nome, idade, número de segurança social e número de telefone em um formulário. O formulário gera um número de conta bancária e detalhes da ramificação. Você pode optar por exibir somente o nome, o número da previdência social, a conta bancária e os detalhes da ramificação no documento de registro.

O documento de configurações de registro de um componente está disponível em suas propriedades. Para acessar as propriedades de um componente, selecione o componente e clique em ![cmppr](assets/cmppr.png) na sobreposição. As propriedades são listadas na barra lateral e você pode encontrar as seguintes configurações nela.

**Configurações de nível de campo**

* **Excluir do documento de registro**: A definição da propriedade true exclui o campo do documento de registro. Esta é uma propriedade com função de script chamada `excludeFromDoR`. Seu comportamento depende de **Excluir campos do DoR se ocultos** propriedade de nível de formulário.

* **Exibir painel como tabela:** Definir a propriedade exibe o painel como tabela no documento de registro se o painel tiver menos de 6 campos. Aplicável somente para painel.
* **Excluir título do Documento de registro:** A configuração da propriedade exclui o título do painel/tabela do documento de registro. Aplicável somente para painel e tabela.
* **Excluir descrição do documento de registro:** A configuração da propriedade exclui a descrição do painel/tabela do documento de registro. Aplicável somente para painel e tabela.
* **[!UICONTROL Paginação]** > **[!UICONTROL Local]**: Determina o local selecionado para posicionar o painel.
   * **[!UICONTROL Local]** > **[!UICONTROL Seguindo anterior]**: Posiciona o painel depois do objeto anterior no painel pai.
   * **[!UICONTROL Local]** > **[!UICONTROL Na área de conteúdo]** > Nome da área de conteúdo: Posiciona o painel na área de conteúdo especificada.
   * **[!UICONTROL Local]** > **[!UICONTROL Parte superior da próxima área de conteúdo]**: Posiciona o painel na parte superior da próxima área de conteúdo.
   * **[!UICONTROL Local]** > **[!UICONTROL Parte superior da área de conteúdo]** > Nome da área de conteúdo: Posiciona o painel na parte superior da área de conteúdo especificada.
   * **[!UICONTROL Local]** > **[!UICONTROL Na página]** > Nome da página principal: Posiciona o painel na página especificada. Se uma quebra de página não for inserida automaticamente, [!DNL AEM Forms] adiciona uma quebra de página.
   * **[!UICONTROL Local]** > **[!UICONTROL Parte superior da próxima página]**: Posiciona o painel na parte superior da próxima página. Se uma quebra de página não for inserida automaticamente, [!DNL AEM Forms] adiciona uma quebra de página.
   * **[!UICONTROL Local]** > **[!UICONTROL Parte superior da página]** > Nome da página principal: Posiciona o painel na parte superior da página, quando a página especificada é renderizada. Se uma quebra de página não for inserida automaticamente, [!DNL AEM Forms] adiciona uma quebra de página.
* **[!UICONTROL Paginação]** > **[!UICONTROL Depois]**: Determina qual área preencher após o posicionamento de um painel. Os seguintes campos estão disponíveis no **[!UICONTROL Depois]** seção:
   * **[!UICONTROL Depois]** > **[!UICONTROL Continuar preenchendo pai]**: Continua unindo dados para todos os objetos que faltam ser preenchidos no painel pai.
   * **[!UICONTROL Depois]** > **[!UICONTROL Ir para a próxima área de conteúdo]**: Começa a preencher a área de conteúdo seguinte após colocar o painel.
   * **[!UICONTROL Depois]** > **[!UICONTROL Ir Para A Área De Conteúdo]** > Nome da área de conteúdo: Começa a preencher a área de conteúdo especificada após colocar o painel.
   * **[!UICONTROL Depois]** > **[!UICONTROL Ir para a próxima página]**: Começa a preencher a próxima página depois de colocar o painel.
   * **[!UICONTROL Depois]** > **[!UICONTROL Ir para a página]** > Nome da página: Começa a preencher a página especificada depois de colocar o painel.
* **[!UICONTROL Paginação]** > **[!UICONTROL Estouro]**: Define um sobrefluxo para um painel ou tabela que se expande pelas páginas. Os seguintes campos estão disponíveis na variável **[!UICONTROL Estouro]** seção:
   * **[!UICONTROL Estouro]** > **[!UICONTROL Nenhum]**: Começa a preencher a próxima página. Se uma quebra de página não for inserida automaticamente, [!DNL AEM Forms] adiciona uma quebra de página.
   * **[!UICONTROL Estouro]** > **[!UICONTROL Ir para a área de conteúdo]** > Nome da área de conteúdo: Começa a preencher a área de conteúdo especificada.
   * **[!UICONTROL Estouro]** > **[!UICONTROL Ir para a página]** > Nome da página: Começa a preencher a página especificada.

Para obter informações sobre como aplicar quebras de página e aplicar várias páginas principais em um Documento de registro, consulte [Aplicar quebra de página em um documento de registro](#apply-page-breaks-in-dor) e [Aplicar várias páginas principais a um documento de registro](#apply-multiple-master-pages-dor).

**Configurações de nível de formulário**

* **Incluir campos não vinculados em DoR:** A configuração da propriedade inclui campos não vinculados do formulário adaptável baseado em esquema no documento de registro. Por padrão, é verdadeiro.
* **Excluir campos de DoR se ocultos:** Defina a propriedade para excluir os campos ocultos do [!UICONTROL Documento de registro] no envio do formulário. Ao ativar [Revalidar no servidor](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form), o servidor recalcula os campos ocultos antes de excluí-los do [!UICONTROL Documento de registro].

## Aplicar uma quebra de página em um documento de registro {#apply-page-breaks-in-dor}

É possível aplicar quebras de página em um Documento de registro usando vários métodos.

Para aplicar uma quebra de página a um Documento de registro:

1. Toque no painel e selecione ![Configurar](/help/forms/using/assets/configure.png)
1. Expandir **[!UICONTROL Documento de registro]** para exibir as propriedades.

1. No **[!UICONTROL Paginação]** seção, toque em ![Pasta](/help/forms/using/assets/folder-icon.png) no **[!UICONTROL Local]** campo.
1. Toque **[!UICONTROL Parte superior da próxima página]** e tocar **[!UICONTROL Selecionar]**. Também é possível tocar em **[!UICONTROL Parte superior da página]**, selecione a página principal e toque em **[!UICONTROL Selecionar]** para aplicar a quebra de página.
1. Toque ![Salvar](/help/forms/using/assets/save_icon.png) para salvar as propriedades.

O painel selecionado é movido para a próxima página.

## Aplicar várias páginas principais a um documento de registro {#apply-multiple-master-pages-dor}

Se o modelo XDP personalizado selecionado incluir várias páginas principais, as propriedades dessas páginas aparecerão na variável [!UICONTROL conteúdo] da seção [!UICONTROL Documento de registro] guia . Para obter mais informações, consulte [Personalizar as informações da marca no documento de registro](#customize-the-branding-information-in-document-of-record).

É possível aplicar várias páginas principais a um Documento de registro ao aplicar diferentes páginas principais aos componentes de um formulário adaptável. Use o [Paginação](#document-of-record-settings) das propriedades Document of Record para aplicar várias páginas principais.

Este é um exemplo de como aplicar várias páginas principais a um Documento de registro: Você faz upload de um modelo XDP que inclui quatro páginas principais para o [!DNL AEM Forms] servidor. [!DNL AEM Forms] aplica as propriedades do modelo ao Documento de registro por padrão. [!DNL AEM Forms] também aplica as primeiras propriedades de página principais no modelo ao Documento de registro.

Para aplicar as propriedades da segunda página principal a um painel e as terceira propriedades da página principal aos painéis a seguir, execute as seguintes etapas:

1. Toque no painel para aplicar a segunda página principal e selecione ![Configurar](assets/cmppr.png).
1. No **[!UICONTROL Paginação]** seção, toque em ![Pasta](/help/forms/using/assets/folder-icon.png) no **[!UICONTROL Local]** campo.
1. Toque **[!UICONTROL Na página]**, selecione a segunda página principal e toque em **[!UICONTROL Selecionar]**.
O AEM Forms aplica a segunda página principal ao painel e a todos os painéis subsequentes no formulário adaptável.
1. No **[!UICONTROL Paginação]** seção, toque em ![Pasta](/help/forms/using/assets/folder-icon.png) no **[!UICONTROL Depois]** campo.
1. Toque **[!UICONTROL Ir para página]**, selecione a terceira página principal e toque em **[!UICONTROL Selecionar]**.
1. Toque ![Salvar](/help/forms/using/assets/save_icon.png) para salvar as propriedades.
O AEM Forms aplica a terceira página principal ao painel e a todos os painéis subsequentes no formulário adaptável.


## Considerações principais ao trabalhar com o documento de registro {#key-considerations-when-working-with-document-of-record}

Lembre-se das considerações e limitações a seguir ao trabalhar no documento de registro de formulários adaptáveis.

* O documento de modelos de registro não suporta Rich Text. Portanto, qualquer rich text no formulário adaptável estático ou nas informações preenchidas pelo usuário final aparece como texto sem formatação no documento de registro.
* Os fragmentos de documento em um formulário adaptável não aparecem no documento de registro. No entanto, fragmentos de formulário adaptáveis são compatíveis.
* Não há suporte para vínculo de conteúdo no documento de registro gerado para o formulário adaptável baseado no Esquema XML.
* A versão localizada do documento de registro é criada sob demanda para uma localidade quando o usuário solicita a renderização do documento de registro. A localização do documento de registro ocorre juntamente com a localização do formulário adaptável. Para obter mais informações sobre a localização do documento de registros e formulários adaptáveis, consulte [Uso AEM fluxo de trabalho de tradução para localizar formulários adaptáveis e documentos de registro](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).
