---
title: Componentes do Adobe Campaign
seo-title: Adobe Campaign Components
description: Ao fazer a integração com o Adobe Campaign, você tem componentes disponíveis para trabalhar com informativos e formulários.
seo-description: When you integrate with Adobe Campaign, you have components available for when working with newsletters and with forms.
uuid: cc9417c9-4cc1-4554-858e-2ecd682dc92f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 5afe864d-5794-4ffa-99e7-a3233f982aff
docset: aem65
exl-id: eeff89c1-41b3-403d-b4bf-c79b09b24d4a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2534'
ht-degree: 80%

---

# Componentes do Adobe Campaign{#adobe-campaign-components}

Ao fazer a integração com o Adobe Campaign, você tem componentes disponíveis para trabalhar com informativos e formulários. Ambos estão descritos neste documento.

>[!CAUTION]
>
>Os componentes de email AEM foram descontinuados. Devido à natureza do email, que mescla conteúdo e estilo, os componentes de email fornecidos prontos para uso pelo AEM se tornam de reutilização limitada para clientes devido à necessidade de implementar estilos personalizados em quaisquer componentes necessários para os projetos.
>
>Os componentes de email podem ser implementados no nível do projeto, e os componentes de email AEM obsoletos ilustram como isso pode ser feito. No entanto, esses componentes obsoletos não devem ser usados em projetos.

## Componentes de informativos do Adobe Campaign {#adobe-campaign-newsletter-components}

Todos os componentes de Campanha seguem as práticas recomendadas descritas em [Práticas recomendadas para modelos de email](/help/sites-administering/best-practices-for-email-templates.md) e se baseiam na linguagem de marcação [HTL](https://helpx.adobe.com/br/experience-manager/htl/using/overview.html) da Adobe.

Ao abrir um informativo/email configurado para integração com o Adobe Campaign, você deve ver os seguintes componentes na seção **Informativo do Adobe Campaign**:

* Cabeçalho (Campaign)
* Imagem (Campaign)
* Link (Campaign)
* Modelo de imagem do Scene7 (Campaign)
* Referência direcionada (Campaign)
* Texto e imagem (Campaign)
* Texto e personalização (Campaign)

Uma descrição desses componentes encontra-se na seção a seguir.

![chlimage_1-81](assets/chlimage_1-81.png)

### Cabeçalho (Campaign) {#heading-campaign}

O componente de cabeçalho pode:

* Exibir o nome da página atual, deixando o campo **Título** em branco.
* Exibir um texto especificado no campo **Título**.

A edição do componente **Cabeçalho (Campaign)** é feita diretamente. Deixe em branco para utilizar o título da página.

![chlimage_1-82](assets/chlimage_1-82.png)

É possível configurar os seguintes itens:

* **Título** Caso deseje usar um nome diferente do título da página, insira-o aqui.

* **Nível de cabeçalho (1, 2, 3, 4)** O nível de cabeçalho com base nos tamanhos de cabeçalho HTML de 1 a 4.

O exemplo a seguir mostra um componente Cabeçalho (Campaign) sendo exibido.

![chlimage_1-83](assets/chlimage_1-83.png)

### Imagem (Campaign) {#image-campaign}

O componente Imagem (Campaign) exibe uma imagem e o texto anexo de acordo com os parâmetros especificados.

Você pode fazer upload de uma imagem e depois editá-la e manipulá-la (por exemplo, recortar, girar, adicionar link/título/texto).

Você pode fazer upload de uma imagem e depois editá-la e manipulá-la (por exemplo, recortar, girar, adicionar link/título/texto). Você pode arrastar e soltar uma imagem do [Localizador de conteúdo](/help/sites-authoring/author-environment-tools.md#thecontentfinderclassicui) diretamente no componente ou na caixa de diálogo Editar. Você também pode clicar duas vezes na área central da caixa de diálogo Editar para navegar pelo seu sistema de arquivos local e fazer upload de uma imagem. As duas guias da caixa de diálogo Editar também controla todas as definições e manipulações da imagem:

![chlimage_1-84](assets/chlimage_1-84.png)

Quando uma imagem é carregada, você pode configurar o seguinte:

* **Mapa**
Para mapear uma imagem, clique em Mapa. É possível selecionar como deseja criar o mapa de imagem (retângulo, polígono e assim por diante) e especificar para onde a área deve apontar.

* **Recortar**
Clique em Recortar para recortar uma imagem. Use o mouse para recortar a imagem.

* **Girar**
Para girar uma imagem, clique em Girar. Clique repetidamente até que a imagem seja girada da maneira que desejar.

* **Apagar** Remova a imagem atual.

* Barra de zoom (somente clássica) Para ampliar e reduzir a imagem, use a barra de rolagem abaixo da imagem (acima dos botões OK e Cancelar)
* **Título** O título da imagem.

* **Texto alternativo** Um texto alternativo que será utilizado na criação de conteúdo acessível.

* **Vincular para** Crie um link para ativos ou outras páginas no seu site.

* **Descrição** Uma descrição da imagem.

* **Tamanho** Define a altura e a largura da imagem.

>[!NOTE]
>
>Você deve inserir informações no campo **Alternar texto** da guia **Avançado**, ou a imagem não poderá ser salva, e a seguinte mensagem de erro será exibida:
>
>`Validation failed. Verify the values of the marked fields.`

O exemplo a seguir mostra um componente Imagem (Campaign) sendo exibido.

![chlimage_1-85](assets/chlimage_1-85.png)

### Link (Campaign) {#link-campaign}

O componente Link (Campaign) permite adicionar um link ao seu informativo. Esse componente só está disponível na interface do usuário clássica, embora você possa adicioná-lo na interface otimizada para toque e abri-lo no modo de compatibilidade.

![chlimage_1-86](assets/chlimage_1-86.png)

É possível configurar os seguintes itens nas guias **Exibir**, **Informações de URL** ou **Avançado**:

* **Legenda do link** A legenda do link. Este é o texto visualizado pelos usuários.

* **Dica de ferramenta do link** Adiciona mais informações sobre como usar o link.

* **LinkType**
Na lista suspensa, selecione entre um 
**URL personalizado** e um **Documento adaptável**. Este campo é obrigatório. Se você selecionar um URL personalizado, será possível fornecer o URL do link. Se você selecionar Documento adaptável, é possível fornecer o caminho do documento.

* **Parâmetro de URL adicional** Adicione qualquer parâmetro de URL adicional. Clique em Adicionar item para adicionar vários itens.

>[!NOTE]
>
>Você deve inserir informações no **Tipo de link** no campo **Informações do URL** ou o componente não poderá ser salvo, e a seguinte mensagem de erro será exibida:
>
>`Validation failed. Verify the values of the marked fields.`

O exemplo a seguir mostra um componente Link (Campaign) sendo exibido.

![chlimage_1-87](assets/chlimage_1-87.png)

### Referência direcionada (Campaign) {#targeted-reference-campaign}

O componente Referência direcionada (Campaign) permite criar uma referência a um parágrafo direcionado.

Nesse componente, você navega até o parágrafo direcionado para selecioná-lo.

Clique no menu suspenso para navegar até o parágrafo que você deseja referenciar. Quando terminar, clique em **OK**.

### Texto e imagem (Campaign) {#text-image-campaign}

O componente Texto e imagem (Campaign) adiciona um bloco de texto e uma imagem.

![chlimage_1-88](assets/chlimage_1-88.png)

Assim como nos componentes Texto e personalização (Campaign) e Imagem (Campaign), é possível configurar:

* **Texto**
Insira o texto. Use a barra de ferramentas para modificar a formatação, criar listas e adicionar links.

* **Imagem**
Arraste uma imagem do localizador de conteúdo ou clique para navegar até uma imagem. Recorte e gire, conforme necessário.

* **Propriedades da imagem** (**Propriedades avançadas de imagem**)
Permite que você especifique o seguinte:

   * **Título** O título do bloco; será exibido ao passar o mouse sobre ele.

   * **Texto alternativo** O texto alternativo que será exibido caso a imagem não possa ser exibida.

   * **Vincular para** Crie um link para ativos ou outras páginas no seu site.

   * **Descrição** Uma descrição da imagem.

   * **Tamanho** Define a altura e a largura da imagem.

>[!NOTE]
>
>O campo **Alternar texto** na guia **Avançado** é necessário, ou o componente não poderá ser salvo, e você verá a seguinte mensagem de erro:
>
>`Validation failed. Verify the values of the marked fields.`

O exemplo a seguir mostra um componente Texto e imagem (Campaign) sendo exibido.

![chlimage_1-89](assets/chlimage_1-89.png)

### Texto e personalização (Campaign) {#text-personalization-campaign}

O componente Texto e personalização (Campaign) permite que você insira um bloco de texto usando um editor WYSIWYG, com a funcionalidade fornecida pelo [Editor de Rich Text](/help/sites-authoring/rich-text-editor.md). Além disso, esse componente permite usar campos de contexto e blocos de personalização disponíveis no Adobe Campaign. Consulte também [Inserir personalização](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#inserting-personalization).

A seleção de ícones permite que você formate o texto, incluindo características de fontes, alinhamento, links, listas e recuo.

Adicione o texto como faria normalmente no editor de rich text. Adicione a personalização selecionando a lista suspensa do Adobe Campaign e escolhendo os campos conforme apropriado.

![chlimage_1-90](assets/chlimage_1-90.png)

Você adiciona os campos de texto e contexto ou os blocos de personalização para criar o conteúdo. Em seguida, selecione o Contexto do cliente para testar os dados nos perfis de persona. Depois de selecionar uma persona, os campos de personalização são automaticamente substituídos pelos dados do perfil selecionado.

>[!NOTE]
>
>Apenas os campos definidos no esquema **nms:seedMember** ou em uma de suas extensões são levados em consideração. Os atributos das tabelas vinculadas a `nms:seedMember` não estão disponíveis.

## Componentes de formulário do Adobe Campaign {#adobe-campaign-form-components}

Você usa componentes do Adobe Campaign para criar um formulário que os usuários preenchem para assinar um informativo, cancelar a assinatura de um informativo ou atualizar seus perfis de usuário. Consulte [Criação de formulários do Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-forms.md) para obter mais informações.

Cada campo de componente pode ser vinculado a um campo de banco de dados do Adobe Campaign. Os campos disponíveis diferem de acordo com o tipo de dados que eles contêm, conforme descrito na seção [Componentes e tipo de dados](#components-and-data-type). Se você estender o esquema de destinatários no Adobe Campaign, os novos campos estarão disponíveis nos componentes cujos tipos de dados corresponderem.

Ao abrir um formulário configurado para integração com o Adobe Campaign, você verá os seguintes componentes na **Adobe Campaign** seção:

* Caixa de seleção (Campaign)
* Campo de dados (Campaign) e Campo de data/HTML5 (Campaign)
* Chave primária criptografada (Campaign)
* Exibição de erro (Campaign)
* Chave de reconciliação oculta (Campaign)
* Campo numérico (Campaign)
* Campo de opções (Campaign)
* Lista de verificação de assinaturas (Campaign)
* Campo de texto (Campaign)

Esta seção descreve cada componente em detalhes.

### Componentes e tipo de dados {#components-and-data-type}

A tabela a seguir descreve os componentes disponíveis para exibir e modificar dados de perfil do Adobe Campaign. Cada componente pode ser mapeado para um campo de perfil do Adobe Campaign para exibir seu valor e atualizar o campo quando o formulário for enviado. Os diferentes componentes só podem ser correspondidos a campos de um tipo de dados apropriado.

<table>
 <tbody>
  <tr>
   <td><p><strong>Componente</strong></p> </td>
   <td><p><strong>Tipo de dados do campo Adobe Campaign</strong></p> </td>
   <td><p><strong>Exemplo de campo</strong></p> </td>
  </tr>
  <tr>
   <td><p>Caixa de seleção (Campaign)</p> </td>
   <td><p>booleano</p> </td>
   <td><p>Não entrar mais em contato (por qualquer canal)</p> </td>
  </tr>
  <tr>
   <td><p>Campo de dados (Campanha)</p> <p>Campo de data/HTML 5 (Campanha)</p> </td>
   <td><p>date</p> </td>
   <td><p>Data de nascimento</p> </td>
  </tr>
  <tr>
   <td><p>Campo numérico (Campaign)</p> </td>
   <td><p>numérico (byte, curto, longo, duplo)</p> </td>
   <td><p>Idade</p> </td>
  </tr>
  <tr>
   <td><p>Campo de opções (Campaign)</p> </td>
   <td><p>byte com valores associados</p> </td>
   <td><p>Sexo</p> </td>
  </tr>
  <tr>
   <td><p>Campo de texto (Campaign)</p> </td>
   <td><p>sequência de caracteres</p> </td>
   <td><p>Email</p> </td>
  </tr>
 </tbody>
</table>

### Configurações comuns à maioria dos componentes {#settings-common-to-most-components}

Os componentes do Adobe Campaign têm configurações que são comuns em todos os componentes (exceto os componentes Chave primária criptografada e Chave de reconciliação oculta).

Na maioria dos componentes, você pode configurar o seguinte:

#### Título e texto {#title-and-text}

* **Título** Se quiser usar um nome diferente do nome do elemento, insira-o aqui.

* **Ocultar título** Marque essa caixa de seleção se não quiser que o título fique visível.

* **Descrição** Adicione uma descrição ao campo para fornecer mais informações para os usuários.

* **Mostrar apenas o valor** Mostra apenas o valor, se houver um

#### Adobe Campaign {#adobe-campaign}

É possível configurar os seguintes itens:

* **Mapeamento** Selecione um campo de personalização do Adobe Campaign, se apropriado.

* **Chave de reconciliação** Marque essa caixa de seleção se esse campo fizer parte da chave de reconciliação.

#### Restrições {#constraints}

* **Obrigatório** - Marque essa caixa de seleção para tornar esse componente obrigatório; ou seja, os usuários devem inserir um valor.
* **Mensagem necessária** - Opcionalmente, adicione uma mensagem informando que o campo é obrigatório.

#### Estilo {#styling}

* **CSS** Insira as classes CSS que você deseja usar para esse componente.

### Caixa de seleção (Campaign) {#checkbox-campaign}

O componente Caixa de seleção (Campaign) permite que o usuário modifique campos de perfil do Adobe Campaign que são do tipo de dados booleano. Por exemplo, você pode ter um componente Caixa de seleção (Campaign) que permite ao destinatário especificar que ele não deseja ser contatado por meio de nenhum canal.

É possível [definir configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components) no componente Caixa de seleção (Campaign).

O exemplo a seguir mostra um componente Caixa de seleção (Campaign) sendo exibido.

![chlimage_1-91](assets/chlimage_1-91.png)

### Campo de dados (Campaign) e Campo de data/HTML 5 (Campaign) {#date-field-campaign-and-date-field-html-campaign}

Use o campo de data para permitir que os destinatários especifiquem uma data. Por exemplo, você pode querer que os destinatários especifiquem suas datas de nascimento. O formato da data corresponde ao formato usado na sua instância do Adobe Campaign.

Além das [configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components), você pode configurar o seguinte:

* **Restrições - Restrição** - Você pode selecionar - **Nenhum** ou **Data** para adicionar a restrição de uma data ou nenhuma restrição. Se você selecionar data, a resposta que os usuários inserirem no campo deverão estar em um formato de data.

* **Mensagem de restrição** - Além disso, é possível adicionar uma mensagem de restrição para que os usuários saibam formatar corretamente suas respostas.
* **Estilo - Largura** - Ajuste a largura do campo clicando ou tocando no botão **+** e **-** ou inserir um número.

O exemplo a seguir mostra um componente Campo de dados (Campaign) com a largura ajustada sendo exibida.

![chlimage_1-92](assets/chlimage_1-92.png)

### Chave primária criptografada (Campaign) {#encrypted-primary-key-campaign}

Esse componente define o nome do parâmetro de URL que conterá o identificador de um perfil do Adobe Campaign (**Identificador de recurso principal** ou **Chave primária criptografada** no Adobe Campaign Standard e 6.1, respectivamente).

Cada formulário que exibe e modifica dados de perfil do Adobe Campaign **deve** incluir um componente Chave primária criptografada.

Você pode configurar o seguinte no componente Chave primária criptografada (Campaign):

* **Título e texto - Nome do elemento** - O padrão é encryptedPK. Você só precisará alterar o nome do elemento quando ele estiver em conflito com o nome de outro elemento no formulário. Dois campos de formulário não podem ter o mesmo nome de elemento.
* **Adobe Campaign - Parâmetro de URL** - Adicione o parâmetro de URL para a EPK. Por exemplo, você pode usar o valor **epk**.

O exemplo a seguir mostra um componente Chave primária criptografada (Campaign) sendo exibido.

![chlimage_1-93](assets/chlimage_1-93.png)

### Exibição de erro (Campaign) {#error-display-campaign}

Esse componente permite exibir erros de back-end. O tratamento de erros do formulário deve ser definido como Encaminhar para que o componente funcione corretamente.

O exemplo a seguir mostra um componente Exibição de erro (Campaign) sendo exibido.

![chlimage_1-94](assets/chlimage_1-94.png)

### Chave de reconciliação oculta (Campaign) {#hidden-reconciliation-key-campaign}

O componente Chave de reconciliação oculta (Campaign) permite adicionar campos ocultos como parte da chave de reconciliação a um formulário.

Você pode configurar os seguintes itens no componente Chave de reconciliação oculta (Campaign):

* **Título e texto - Nome do elemento** - O padrão é reconcilKey. Você só precisará alterar o nome do elemento quando ele estiver em conflito com o nome de outro elemento no formulário. Dois campos de formulário não podem ter o mesmo nome de elemento.
* **Adobe Campaign - Mapeamento** - Mapear para um campo de personalização do Adobe Campaign.

O exemplo a seguir mostra um componente Chave de reconciliação oculta (Campaign) sendo exibido.

![chlimage_1-95](assets/chlimage_1-95.png)

### Campo numérico (Campaign) {#numeric-field-campaign}

Use o campo numérico para permitir que os destinatários insiram números, por exemplo, suas idades.

Além das [configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components), você pode configurar o seguinte:

* **Restrições - Restrição** menu suspenso Você pode selecionar - **Nenhum** ou **Numérico -** para adicionar a restrição de um número ou nenhuma restrição. Se você selecionar um número, a resposta que os usuários inserirem no campo deverá ser numérica.

* **Mensagem de restrição** - Além disso, é possível adicionar uma mensagem de restrição para que os usuários saibam formatar corretamente suas respostas.
* **Estilo - Largura** - Ajuste a largura do campo clicando ou tocando no botão **+** e **-** ou inserir um número.

O exemplo a seguir mostra um componente Campo numérico (Campaign) com a largura configurada sendo exibida.

![chlimage_1-96](assets/chlimage_1-96.png)

### Campo de opções (Campaign) {#option-field-campaign}

Essa lista suspensa permite selecionar uma opção, por exemplo, o sexo ou o status de um destinatário.

É possível [definir configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components) no componente Campo de opções (Campaign). Para preencher a lista suspensa, selecione o campo apropriado nos campos de personalização do Adobe Campaign, clicando ou tocando no símbolo do Adobe Campaign e navegando até o campo.

O exemplo a seguir mostra um componente Campo de opções (Campaign) sendo exibido.

![chlimage_1-97](assets/chlimage_1-97.png)

### Lista de verificação de assinaturas (Campaign) {#subscriptions-checklist-campaign}

Use o componente **Lista de verificação de assinaturas (Campaign)** para modificar as assinaturas associadas a um perfil do Adobe Campaign.

Quando adicionado a um formulário, esse componente exibe todas as assinaturas disponíveis como caixas de seleção e permite que o usuário selecione as assinaturas desejadas. Quando os usuários enviam o formulário, esse componente inscreve o usuário ou cancela a assinatura dos serviços selecionados, dependendo do tipo de ação de formulário (**Adobe Campaign: Inscrever-se nos Serviços** ou **Adobe Campaign: Cancelar assinatura dos serviços**).

>[!NOTE]
>
>O componente não verifica quais serviços já foram assinados/cancelados pelo usuário.

É possível [definir configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components) no componente Lista de verificação de assinaturas (Campaign). (Não há configurações do Adobe Campaign disponíveis para esse componente.)

O exemplo a seguir mostra um componente Lista de verificação de assinaturas (Campaign) sendo exibido.

![chlimage_1-98](assets/chlimage_1-98.png)

### Campo de texto (Campaign) {#text-field-campaign}

O componente Campo de texto (Campaign), que permite inserir dados do tipo sequência de caracteres, como nome, sobrenome, endereço, endereço de email e assim por diante.

Além das [configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components), você pode configurar o seguinte:

* **Restrições - Restrição** - suspenso - Você pode selecionar - **Nenhum**, **Email**, **Nome** (sem tremas) para adicionar a restrição de um endereço de email, nome ou nenhuma restrição. Se você selecionar um email, a resposta que os usuários inserirem no campo deverá ser um endereço de email. Se você selecionar um nome, a resposta deverá ser um nome (tremas não são permitidos).

* **Mensagem de restrição** - Além disso, é possível adicionar uma mensagem de restrição para que os usuários saibam formatar corretamente suas respostas.
* **Estilo - Largura** - Ajuste a largura do campo clicando ou tocando no botão **+** e **-** ou inserir um número.

O exemplo a seguir mostra um componente Campo de texto (Campaign) sendo exibido.

![chlimage_1-99](assets/chlimage_1-99.png)
