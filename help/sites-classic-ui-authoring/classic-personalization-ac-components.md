---
title: Componentes do Adobe Campaign
description: Ao integrar com o Adobe Campaign, você tem componentes disponíveis para o ao trabalhar com boletins informativos e formulários.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: eeff89c1-41b3-403d-b4bf-c79b09b24d4a
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 4%

---

# Componentes do Adobe Campaign{#adobe-campaign-components}

Ao integrar com o Adobe Campaign, você tem componentes disponíveis para o ao trabalhar com boletins informativos e formulários. Ambos estão descritos neste documento.

>[!CAUTION]
>
>Os componentes de email do AEM foram descontinuados. Devido à natureza do email, que mescla conteúdo e estilo, os componentes de email fornecidos prontos para uso pelo AEM tornam-se de reutilização limitada para os clientes, devido à necessidade de implementar estilos personalizados em quaisquer componentes que sejam necessários para projetos.
>
>Os componentes de email podem ser implementados no nível do projeto, e os componentes de email do AEM obsoletos ilustram como isso pode ser feito. No entanto, não use esses componentes obsoletos em projetos.

## Componentes do informativo do Adobe Campaign {#adobe-campaign-newsletter-components}

Todos os componentes do Campaign seguem as práticas recomendadas descritas em [Práticas recomendadas para modelos de email](/help/sites-administering/best-practices-for-email-templates.md) e se baseiam na linguagem de marcação Adobe [HTL](https://helpx.adobe.com/br/experience-manager/htl/using/overview.html).

Ao abrir um boletim informativo/email configurado para integração com o Adobe Campaign, você deve ver os seguintes componentes na seção **Informativo da Adobe Campaign**:

* Cabeçalho (Campanha)
* Imagem (Campanha)
* Link (Campanha)
* Modelo de imagem do Scene7 (Campanha)
* Referência direcionada (Campaign)
* Texto e Imagem (Campanha)
* Texto e personalização (Campanha)

Uma descrição desses componentes está na seção a seguir.

![chlimage_1-81](assets/chlimage_1-81.png)

### Cabeçalho (Campanha) {#heading-campaign}

O componente de cabeçalho pode:

* Exiba o nome da página atual deixando o campo **Título** em branco.
* Exibir um texto especificado no campo **Título**.

Você edita o componente **Cabeçalho (Campanha)** diretamente. Deixe em branco para utilizar título da página.

![chlimage_1-82](assets/chlimage_1-82.png)

Você pode configurar o seguinte:

* **Título**
Se quiser usar um nome diferente do título da página, insira-o aqui.

* **Nível do cabeçalho (1, 2, 3, 4)**
O nível do cabeçalho com base nos tamanhos dos cabeçalhos HTML 1-4.

O exemplo a seguir mostra um componente de Cabeçalho (Campanha) sendo exibido.

![chlimage_1-83](assets/chlimage_1-83.png)

### Imagem (Campanha) {#image-campaign}

O componente de imagem (campanha) exibe uma imagem e o texto de acompanhamento de acordo com os parâmetros especificados.

É possível carregar uma imagem, editá-la e manipulá-la (por exemplo, cortar, girar, adicionar link/título/texto).

É possível carregar uma imagem, editá-la e manipulá-la (por exemplo, cortar, girar, adicionar link/título/texto). Você pode arrastar e soltar uma imagem do [Localizador de Conteúdo](/help/sites-authoring/author-environment-tools.md#thecontentfinderclassicui) diretamente no componente ou em sua caixa de diálogo Editar. Você também pode clicar duas vezes na área central da caixa de diálogo Editar para navegar pelo sistema de arquivos local e fazer upload de uma imagem. As duas guias da caixa de diálogo Editar também controlam todas as definições e manipulações da imagem:

![chlimage_1-84](assets/chlimage_1-84.png)

Quando uma imagem é carregada, você pode configurar o seguinte:

* **Mapa**
Para mapear uma imagem, selecione Mapear. Você pode especificar como deseja criar o mapa de imagem (retângulo, polígono etc.) e onde a área deve apontar.

* **Cortar**
Selecione Cortar para recortar uma imagem. Use o mouse para cortar a imagem.

* **Girar**
Para girar uma imagem, selecione Girar. Use repetidamente até que a imagem seja girada da maneira desejada.

* **Limpar**
Remover a imagem atual.

* Barra de zoom (apenas clássica)
Para ampliar e reduzir a imagem, use a barra deslizante abaixo da imagem (acima dos botões OK e Cancelar)
* **Título**
O título da imagem.

* **Texto Alternativo**
Um texto alternativo a ser usado ao criar conteúdo acessível.

* **Vincular a**
Crie um link para ativos ou outras páginas no seu site.

* **Descrição**
Uma descrição da imagem.

* **Tamanho**
Define a altura e a largura da imagem.

>[!NOTE]
>
>Insira informações no campo **Alt Text** da guia **Avançado** ou a imagem não pode ser salva e você verá a seguinte mensagem de erro:
>
>`Validation failed. Verify the values of the marked fields.`
>

O exemplo a seguir mostra um componente de Imagem (Campanha) sendo exibido.

![chlimage_1-85](assets/chlimage_1-85.png)

### Link (Campanha) {#link-campaign}

O componente Link (Campanha) permite adicionar um link ao seu informativo. Esse componente só está disponível na interface de usuário clássica, embora você possa adicionar um na interface de usuário otimizada para toque e abri-lo no modo de compatibilidade.

![chlimage_1-86](assets/chlimage_1-86.png)

Você pode configurar as seguintes opções nas guias **Exibir**, **Informações sobre URL** ou **Avançado**:

* **Legenda do link**
A legenda do link. Esse é o texto que os usuários veem.

* **Vincular ToolTip**
Adiciona mais informações sobre como usar o link.

* **TipoLink**
Na lista suspensa, selecione entre um **URL personalizado** e um **Documento adaptável**. Este campo é obrigatório. Se você selecionar URL personalizado, poderá fornecer o URL do link. Se você selecionar Documento adaptável, poderá fornecer o caminho do documento.

* **Parâmetro de URL Adicional**
Adicione quaisquer parâmetros de URL adicionais. Clique em Adicionar item para adicionar vários itens.

>[!NOTE]
>
>Digite informações no campo **Tipo de link** da guia **Informações de URL** ou o componente não pode ser salvo e você verá a seguinte mensagem de erro:
>
>`Validation failed. Verify the values of the marked fields.`
>

O exemplo a seguir mostra um componente Link (Campanha) sendo exibido.

![chlimage_1-87](assets/chlimage_1-87.png)

### Referência direcionada (Campaign) {#targeted-reference-campaign}

O componente Referência direcionada (Campanha) permite criar uma referência a um parágrafo direcionado.

Neste componente, navegue até o parágrafo de destino para selecioná-lo.

Clique no menu suspenso para navegar até o parágrafo que deseja referenciar. Quando terminar, clique em **OK**.

### Texto e Imagem (Campanha) {#text-image-campaign}

O componente Texto e imagem (Campanha) adiciona um bloco de texto e uma imagem.

![chlimage_1-88](assets/chlimage_1-88.png)

Assim como nos componentes Texto e Personalization (Campaign) e Imagem (Campaign), você pode configurar:

* **Texto**
Insira o texto. Use a barra de ferramentas para modificar a formatação, criar listas e adicionar links.

* **Imagem**
Arraste uma imagem do localizador de conteúdo ou clique em para navegar até uma imagem. Recorte ou gire conforme necessário.

* **Propriedades da Imagem** (**Propriedades Avançadas da Imagem**)
Permite especificar o seguinte:

   * **Título**
O título do bloco; é mostrado por mouseover.

   * **Texto Alternativo**
Texto alternativo a ser mostrado se a imagem não puder ser exibida.

   * **Vincular a**
Crie um link para ativos ou outras páginas no seu site.

   * **Descrição**
Uma descrição da imagem.

   * **Tamanho**
Define a altura e a largura da imagem.

>[!NOTE]
>
>O campo **Texto alternativo** da guia **Avançado** é obrigatório ou o componente não pode ser salvo e você verá a seguinte mensagem de erro:
>
>`Validation failed. Verify the values of the marked fields.`
>

O exemplo a seguir mostra um componente de Texto e imagem (Campanha) sendo exibido.

![chlimage_1-89](assets/chlimage_1-89.png)

### Texto e personalização (Campanha) {#text-personalization-campaign}

O componente Text &amp; Personalization (Campaign) permite inserir um bloco de texto usando um editor WYSIWYG, com a funcionalidade fornecida pelo [editor de Rich Text](/help/sites-authoring/rich-text-editor.md). Além disso, esse componente permite usar campos de contexto e blocos de personalização disponíveis no Adobe Campaign. Consulte também [Inserção do Personalization](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#inserting-personalization).

A seleção de ícones permite formatar o texto, incluindo características de fonte, alinhamento, links, listas e recuo.

Adicione texto como você faria normalmente no editor de rich text. Adicione personalização ao selecionar a lista suspensa Adobe Campaign e os campos conforme apropriado.

![chlimage_1-90](assets/chlimage_1-90.png)

Adicione os campos de texto e contexto ou blocos de personalização para criar o conteúdo. Em seguida, selecione o Client Context para testar os dados nos perfis de persona. Após selecionar um perfil, os campos de personalização são substituídos automaticamente pelos dados do perfil selecionado.

>[!NOTE]
>
>Somente os campos definidos no esquema **nms:seedMember** ou em uma de suas extensões são considerados. Os atributos das tabelas vinculadas a `nms:seedMember` não estão disponíveis.

## Componentes de formulário do Adobe Campaign {#adobe-campaign-form-components}

Use os componentes do Adobe Campaign para criar um formulário que os usuários preenchem para assinar um boletim informativo, cancelar a assinatura de um boletim informativo ou atualizar seus perfis de usuário. Consulte [Criando o Adobe Campaign Forms](/help/sites-classic-ui-authoring/classic-personalization-ac-forms.md) para obter mais informações.

Cada campo de componente pode ser vinculado a um campo de banco de dados do Adobe Campaign. Os campos disponíveis diferem de acordo com o tipo de dados que contêm, conforme descrito na seção [Componentes e Tipo de Dados](#components-and-data-type). Se você estender o esquema de recipient no Adobe Campaign, os novos campos estarão disponíveis nos componentes cujos tipos de dados correspondem.

Ao abrir um formulário configurado para integração com o Adobe Campaign, você verá os seguintes componentes na seção **Adobe Campaign**:

* Caixa de seleção (Campanha)
* Campo de data (Campanha) e Campo de data/HTML5 (Campanha)
* Chave primária criptografada (Campanha)
* Exibição de erro (Campaign)
* Chave de reconciliação oculta (Campanha)
* Campo numérico (Campanha)
* Campo de opções (Campanha)
* Lista de verificação de assinaturas (Campanha)
* Campo de texto (Campanha)

Esta seção descreve cada componente em detalhes.

### Componentes e tipo de dados {#components-and-data-type}

A tabela a seguir descreve os componentes que estão disponíveis para exibir e modificar dados de perfil do Adobe Campaign. Cada componente pode ser mapeado para um campo de perfil do Adobe Campaign para exibir seu valor e atualizar o campo quando o formulário for enviado. Os diferentes componentes só podem ser correspondidos a campos de um tipo de dados apropriado.

<table>
 <tbody>
  <tr>
   <td><p><strong>Componente</strong></p> </td>
   <td><p><strong>Tipo de dados do campo do Adobe Campaign</strong></p> </td>
   <td><p><strong>Exemplo de campo</strong></p> </td>
  </tr>
  <tr>
   <td><p>Caixa de seleção (Campanha)</p> </td>
   <td><p>booleano</p> </td>
   <td><p>Não entrar mais em contato (por qualquer canal)</p> </td>
  </tr>
  <tr>
   <td><p>Campo de dados (Campanha)</p> <p>Campo de data/HTML 5 (Campanha)</p> </td>
   <td><p>data</p> </td>
   <td><p>Data de nascimento</p> </td>
  </tr>
  <tr>
   <td><p>Campo numérico (Campanha)</p> </td>
   <td><p>numérico (byte, curto, longo, duplo)</p> </td>
   <td><p>Idade</p> </td>
  </tr>
  <tr>
   <td><p>Campo de opções (Campanha)</p> </td>
   <td><p>byte com valores associados</p> </td>
   <td><p>Sexo</p> </td>
  </tr>
  <tr>
   <td><p>Campo de texto (Campanha)</p> </td>
   <td><p>string</p> </td>
   <td><p>Email</p> </td>
  </tr>
 </tbody>
</table>

### Configurações comuns à maioria dos componentes {#settings-common-to-most-components}

Os componentes do Adobe Campaign têm configurações comuns em todos os componentes (exceto os componentes Chave primária criptografada e Chave de reconciliação oculta).

Na maioria dos componentes, é possível configurar o seguinte:

#### Título e texto {#title-and-text}

* **Título**
Se quiser usar um nome diferente do nome do elemento, insira-o aqui.

* **Ocultar título**
Marque essa caixa de seleção se não quiser que o título fique visível.

* **Descrição**
Adicione uma descrição ao campo para fornecer mais informações aos usuários.

* **Mostrar apenas o valor**
Mostra apenas o valor, se houver um

#### Adobe Campaign {#adobe-campaign}

Você pode configurar o seguinte:

* **Mapeamento**
Selecione um campo de personalização do Adobe Campaign, se apropriado.

* **Chave de reconciliação**
Marque esta caixa de seleção se este campo fizer parte da chave de reconciliação.

#### Restrições {#constraints}

* **Obrigatório** - Marque esta caixa de seleção para tornar este componente obrigatório; ou seja, os usuários devem inserir um valor.
* **Mensagem Necessária** - Opcionalmente, adicione uma mensagem informando que o campo é obrigatório.

#### Estilo {#styling}

* **CSS**
Insira as classes CSS que você deseja usar para este componente.

### Caixa de seleção (Campanha) {#checkbox-campaign}

O componente Caixa de seleção (Campanha) permite que o usuário modifique campos de perfil do Adobe Campaign que são do tipo de dados booleano. Por exemplo, você pode ter um componente Caixa de seleção (Campanha) que permite que o recipient especifique que não deseja ser contatado por meio de nenhum canal.

Você pode [definir configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components) no componente Caixa de seleção (Campanha).

O exemplo a seguir mostra um componente Caixa de seleção (Campanha) sendo exibido.

![chlimage_1-91](assets/chlimage_1-91.png)

### Campo de data (Campanha) e Campo de data/HTML 5 (Campanha) {#date-field-campaign-and-date-field-html-campaign}

Use o campo de data para permitir que os destinatários definam uma data; por exemplo, você pode desejar que os destinatários especifiquem suas datas de nascimento. O formato de data corresponde ao formato usado na instância do Adobe Campaign.

Além das [configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components), você pode definir o seguinte:

* **Restrições - Restrição** - Você pode selecionar - **Nenhuma** ou **Data** para adicionar a restrição de uma data ou nenhuma restrição. Se você selecionar data, os usuários de resposta inseridos no campo deverão estar em um formato de data.

* **Mensagem de Restrição** - Além disso, você pode adicionar uma mensagem de restrição para que os usuários saibam como formatar corretamente suas respostas.
* **Estilo - Largura** - Ajuste a largura do campo clicando ou tocando nos ícones **+** e **-** ou digitando um número.

O exemplo a seguir mostra um componente Campo de data (Campanha) com a largura ajustada sendo exibida.

![chlimage_1-92](assets/chlimage_1-92.png)

### Chave primária criptografada (Campanha) {#encrypted-primary-key-campaign}

Este componente define o nome do parâmetro de URL que conterá o identificador de um perfil do Adobe Campaign (**Identificador de Recurso Principal** ou **Chave primária criptografada** no Adobe Campaign Standard e 6.1, respectivamente).

Cada formulário exibindo e modificando os dados de perfil do Adobe Campaign **deve** incluir um componente de Chave Primária Criptografada.

Você pode configurar o seguinte no componente Chave primária criptografada (Campaign):

* **Título e Texto - Nome do Elemento** - O padrão é encryptedPK. Você só precisa alterar o nome do elemento quando ele estiver em conflito com o nome de outro elemento no formulário. Nenhum campo de formulário pode ter o mesmo nome de elemento.
* **Adobe Campaign - Parâmetro de URL** - Adicione o parâmetro de URL para o EPK. Por exemplo, você pode usar o valor **epk**.

O exemplo a seguir mostra um componente de Chave primária criptografada (Campanha) que está sendo exibido.

![chlimage_1-93](assets/chlimage_1-93.png)

### Exibição de erro (Campaign) {#error-display-campaign}

Esse componente permite exibir erros de backend. A manipulação de erros do formulário precisa ser definida como Encaminhar para que o componente funcione corretamente.

O exemplo a seguir mostra um componente de Exibição de erro (Campanha) sendo exibido.

![chlimage_1-94](assets/chlimage_1-94.png)

### Chave de reconciliação oculta (Campanha) {#hidden-reconciliation-key-campaign}

O componente Chave de reconciliação oculta (Campanha) permite adicionar campos ocultos como parte da chave de reconciliação a um formulário.

Você pode configurar o seguinte no componente Chave de reconciliação oculta (Campanha):

* **Título e Texto - Nome do Elemento** - O padrão é reconciliarKey. Você só precisa alterar o nome do elemento quando ele estiver em conflito com o nome de outro elemento no formulário. Nenhum campo de formulário pode ter o mesmo nome de elemento.
* **Adobe Campaign - Mapeamento** - Mapear para um campo de personalização do Adobe Campaign.

O exemplo a seguir mostra um componente Chave de reconciliação oculta (Campanha) que está sendo exibido.

![chlimage_1-95](assets/chlimage_1-95.png)

### Campo numérico (Campanha) {#numeric-field-campaign}

Use o campo numérico para permitir que os recipients insiram números, por exemplo, sua idade.

Além das [configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components), você pode definir o seguinte:

* **Restrições - Menu suspenso Restrição**
Você pode selecionar - **Nenhum** ou **Numérico -** para adicionar a restrição de um número ou nenhuma restrição. Se você selecionar número, os usuários de resposta inseridos no campo deverão ser numéricos.

* **Mensagem de Restrição** - Além disso, você pode adicionar uma mensagem de restrição para que os usuários saibam como formatar corretamente suas respostas.
* **Estilo - Largura** - Ajuste a largura do campo clicando ou tocando nos ícones **+** e **-** ou digitando um número.

O exemplo a seguir mostra um componente de Campo numérico (Campanha) com a largura configurada sendo exibida.

![chlimage_1-96](assets/chlimage_1-96.png)

### Campo de opções (Campanha) {#option-field-campaign}

Essa lista suspensa permite selecionar uma opção; por exemplo, o gênero ou o status de um recipient.

Você pode [definir configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components) no componente Campo de Opções (Campanha). Para preencher a lista suspensa, selecione o campo apropriado nos campos de personalização do Adobe Campaign clicando ou tocando no símbolo da Adobe Campaign e navegando até o campo.

O exemplo a seguir mostra um componente Campo de opções (Campanha) sendo exibido.

![chlimage_1-97](assets/chlimage_1-97.png)

### Lista de verificação de assinaturas (Campanha) {#subscriptions-checklist-campaign}

Use o componente **Lista de Verificação de Assinaturas (Campanha)** para modificar as assinaturas associadas a um perfil do Adobe Campaign.

Quando adicionado a um formulário, esse componente exibe todas as assinaturas disponíveis como caixas de seleção e permite que o usuário selecione as assinaturas desejadas. Quando os usuários enviam o formulário, este componente faz a assinatura do usuário ou cancela a assinatura do usuário nos serviços selecionados, dependendo do tipo de ação de formulário (**Adobe Campaign: Assinar Serviços** ou **Adobe Campaign: Cancelar Assinatura de Serviços**).

>[!NOTE]
>
>O componente não verifica quais serviços o usuário já assinou/cancelou a assinatura.

Você pode [definir configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components) no componente Lista de verificação de assinaturas (Campanha). (Não há configurações do Adobe Campaign disponíveis para este componente.)

O exemplo a seguir mostra um componente Lista de verificação de assinaturas (Campanha) que está sendo exibido.

![chlimage_1-98](assets/chlimage_1-98.png)

### Campo de texto (Campanha) {#text-field-campaign}

O componente Campo de texto (Campanha) que permite inserir dados do tipo string, como nome, sobrenome, endereço, endereço de email e assim por diante.

Além das [configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components), você pode definir o seguinte:

* **Restrições - Restrição** - lista suspensa - Você pode selecionar - **Nenhum**, **Email**, **Nome** (sem umlauts) para adicionar a restrição de um endereço de email, nome ou nenhuma restrição. Se você selecionar email, os usuários de resposta inseridos no campo deverão ser um endereço de email. Se você selecionar name, ele deverá ser um nome (umlauts não são permitidos).

* **Mensagem de Restrição** - Além disso, você pode adicionar uma mensagem de restrição para que os usuários saibam como formatar corretamente suas respostas.
* **Estilo - Largura** - Ajuste a largura do campo clicando ou tocando nos ícones **+** e **-** ou digitando um número.

O exemplo a seguir mostra um componente Campo de texto (Campanha) sendo exibido.

![chlimage_1-99](assets/chlimage_1-99.png)
