---
title: Integração com componentes do Adobe Campaign
description: Ao fazer a integração com o Adobe Campaign, você tem componentes disponíveis para trabalhar com informativos e formulários.
uuid: a858d5ca-aa6e-4bde-92db-a6dcd8b48ae6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9da34dab-7e89-4127-ab26-532687746b2a
docset: aem65
exl-id: d1132fcd-e6a0-44a2-8753-d250f68fbd78
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '2828'
ht-degree: 4%

---

# Componentes do Adobe Campaign{#adobe-campaign-components}

Ao fazer a integração com o Adobe Campaign, você tem componentes disponíveis para trabalhar com informativos e formulários. Ambos estão descritos neste documento.

>[!CAUTION]
>
>Os componentes de email AEM foram descontinuados. Devido à natureza do email, que mescla conteúdo e estilo, os componentes de email fornecidos prontos para uso pelo AEM se tornam de reutilização limitada para clientes devido à necessidade de implementar estilos personalizados em quaisquer componentes necessários para os projetos.
>
>Os componentes de email podem ser implementados no nível do projeto, e os componentes de email AEM obsoletos ilustram como isso pode ser feito. No entanto, esses componentes obsoletos não devem ser usados em projetos.

## Componentes do informativo do Adobe Campaign {#adobe-campaign-newsletter-components}

Todos os componentes do Campaign seguem as práticas recomendadas descritas em [Práticas recomendadas para modelos de email](/help/sites-administering/best-practices-for-email-templates.md) e são baseados na linguagem de marcação Adobe [HTL](https://helpx.adobe.com/br/experience-manager/htl/using/overview.html).

Ao abrir um informativo/email configurado para integração com o Adobe Campaign, você deve ver os seguintes componentes na **Informativo do Adobe Campaign** seção:

* Cabeçalho (Campanha)
* Imagem (Campanha)
* Link (Campanha)
* Modelo de imagem do Scene7 (Campanha)
* Referência direcionada (Campaign)
* Texto e Imagem (Campanha)
* Texto e personalização (Campanha)

Uma descrição desses componentes está na seção a seguir.

Os componentes são exibidos da seguinte maneira:

![chlimage_1-43](assets/chlimage_1-43.png)

### Cabeçalho (Campanha) {#heading-campaign}

O componente de cabeçalho pode:

* Exibir o nome da página atual, deixando a variável **Título** campo em branco.
* Exibir um texto especificado na variável **Título** campo.

Você edita a variável **Cabeçalho (Campaign)** componente diretamente. Deixe em branco para utilizar título da página.

![chlimage_1-44](assets/chlimage_1-44.png)

Você pode configurar o seguinte:

* **Título**
Se quiser usar um nome diferente do título da página, insira-o aqui.

* **Nível de cabeçalho (1, 2, 3, 4)**
O nível de cabeçalho com base nos tamanhos de cabeçalho de HTML de 1 a 4.

O exemplo a seguir mostra um componente Cabeçalho (Campaign) sendo exibido.

![chlimage_1-45](assets/chlimage_1-45.png)

### Imagem (Campanha) {#image-campaign}

O componente de imagem (campanha) exibe uma imagem e o texto respectivo de acordo com os parâmetros especificados.

Você pode fazer upload de uma imagem, em seguida, editá-la e manipulá-la (por exemplo, recortar, girar, adicionar link/título/texto).

Você pode arrastar e soltar uma imagem do [Navegador de ativos](/help/sites-authoring/author-environment-tools.md#assetsbrowsertouchoptimizedui) diretamente no componente ou em seu [Caixa de diálogo Configurar](/help/sites-authoring/editing-content.md#editconfigurecopycutdeletepastetouchoptimizedui). Também é possível fazer upload de uma imagem na caixa de diálogo Configurar ; essa caixa de diálogo também controla todas as definições e manipulações da imagem:

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>Você deve inserir informações no **Texto alternativo** ou a imagem não pode ser salva.

Após a imagem ser carregada (e não antes), você pode usar [edição no local](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui) para cortar/girar a imagem conforme necessário:

![](do-not-localize/chlimage_1-10.png)

>[!NOTE]
>
>O editor local usa o tamanho e a proporção original da imagem durante a edição. Também é possível especificar as propriedades de altura e largura. Qualquer restrição de tamanho e aspecto definida nas propriedades será aplicada ao salvar as alterações de edição.
>
>Dependendo do seu caso, restrições mínimas e máximas também podem ser impostas pelo [design da página](/help/sites-developing/designer.md); são desenvolvidos durante a implementação do projeto.

Várias opções adicionais estão disponíveis no modo de edição de tela cheia; por exemplo, mapa e zoom:

![](do-not-localize/chlimage_1-11.png)

Quando uma imagem é carregada, você pode configurar o seguinte:

* **Mapa**
Para mapear uma imagem, selecione Mapa. Você pode especificar como deseja criar o mapa de imagem (retângulo, polígono e assim por diante) e para onde a área deve apontar.

* **Cortar**
Selecione Recortar para recortar uma imagem. Use o mouse para recortar a imagem.

* **Girar**
Para girar uma imagem, selecione Girar. Use repetidamente até que a imagem seja girada da maneira que desejar.

* **Limpar**
Remova a imagem atual.

* Barra de zoom (somente clássica) Para aumentar e diminuir o zoom da imagem, use a barra de rolagem abaixo da imagem (acima dos botões OK e Cancelar)
* **Título**
O título da imagem.

* **Texto alternativo**
Um texto alternativo para usar na criação de conteúdo acessível.

* **Vincular ao**
Crie um link para ativos ou outras páginas no seu site.

* **Descrição**
Uma descrição da imagem.

* **Tamanho**
Define a altura e a largura da imagem.

>[!NOTE]
>
>Você deve inserir informações no **Texto alternativo** no campo **Avançado** ou a imagem não poderá ser salva e você verá a seguinte mensagem de erro:
>
>`Validation failed. Verify the values of the marked fields.`

O exemplo a seguir mostra um componente de Imagem (Campaign) sendo exibido.

![chlimage_1-47](assets/chlimage_1-47.png)

### Link (Campanha) {#link-campaign}

O componente Link (Campaign) permite adicionar um link ao seu informativo.

Você pode configurar o seguinte no **Exibir**, **Informações do URL** ou **Avançado** guias:

* **Legenda do link**
A legenda do link. Este é o texto que os usuários veem.

* **Dica da ferramenta Link**
Adiciona informações adicionais sobre como usar o link.

* **LinkType**
Na lista suspensa, selecione entre um 
**URL personalizado** e um **Documento adaptável**. Este campo é obrigatório. Se você selecionar URL personalizado, é possível fornecer o URL do link. Se você selecionar Documento adaptável, poderá fornecer o caminho do documento.

* **Parâmetro de URL adicional**
Adicione quaisquer parâmetros de URL adicionais. Clique em Adicionar item para adicionar vários itens.

>[!NOTE]
>
>Você deve inserir informações no **Tipo de link** no campo **Informações do URL** ou o componente não poderá ser salvo, e a seguinte mensagem de erro será exibida:
>
>`Validation failed. Verify the values of the marked fields.`

O exemplo a seguir mostra um componente Link (Campaign) sendo exibido.

![chlimage_1-48](assets/chlimage_1-48.png)

### Modelo de imagem do Dynamic Media Classic (Scene7) (Campaign) {#scene-image-template-campaign}

Os Modelos de imagem do Dynamic Media Classic (Scene7) são arquivos de imagem em camadas, onde o conteúdo e as propriedades podem ser parametrizadas para oferecer variabilidade. O **[!UICONTROL Modelo de imagem]** permite usar modelos do Scene7 em informativos e alterar os valores dos parâmetros do modelo. Além disso, você pode usar variáveis de metadados do Adobe Campaign dentro dos parâmetros, para que cada usuário experimente a imagem de uma maneira personalizada.

![chlimage_1-49](assets/chlimage_1-49.png)

Clique em **Editar** para configurar o componente. Você pode definir as configurações descritas nesta seção. Este modelo de Imagem do Scene7 é descrito detalhadamente em [Componente de modelo de imagem do Scene7](/help/assets/scene7.md#image-template).

Além disso, o painel de parâmetros lista todos os parâmetros do modelo que foram definidos para o modelo no Scene7. Para cada um desses parâmetros, é possível adaptar o valor, inserir variáveis ou redefini-las com o valor padrão.

![chlimage_1-50](assets/chlimage_1-50.png)

### Referência direcionada (Campaign) {#targeted-reference-campaign}

O componente Referência direcionada (Campaign) permite criar uma referência a um parágrafo direcionado.

Nesse componente, você navega até o parágrafo direcionado para selecioná-lo.

Clique no ícone de pasta para navegar até o parágrafo que deseja referenciar. Quando terminar, clique na marca de seleção.

### Texto e Imagem (Campanha) {#text-image-campaign}

O componente Texto e imagem (Campaign) adiciona um bloco de texto e uma imagem.

Ao clicar para configurar o componente, você seleciona Texto ou Imagem.

![chlimage_1-51](assets/chlimage_1-51.png)

Selecionar **Texto** exibe um editor em linha:

![](do-not-localize/chlimage_1-12.png)

Selecionar **Imagem** exibe o editor local de imagens:

![](do-not-localize/chlimage_1-13.png)

Consulte [Componente de imagem (Campaign)](#image-campaign) para obter mais informações sobre como trabalhar com imagens. Consulte [Componente Texto e personalização (Campaign)](#text-personalization-campaign) para obter mais informações sobre como trabalhar com texto.

Assim como nos componentes Texto e personalização (Campaign) e Imagem (Campaign) , é possível configurar:

* **Texto**
Inserir texto. Use a barra de ferramentas para modificar a formatação, criar listas e adicionar links.

* **Imagem**
Arraste uma imagem do localizador de conteúdo ou clique para navegar até uma imagem. Recorte ou gire, conforme necessário.

* **Propriedades da imagem** (**Propriedades avançadas de imagem**) Permite que você especifique o seguinte:

   * **Título**
O título do bloco; será exibido ao passar o mouse.

   * **Texto alternativo**
Texto alternativo a ser exibido se a imagem não puder ser exibida.

   * **Link para**
Crie um link para ativos ou outras páginas no seu site.

   * **Descrição**
Uma descrição da imagem.

   * **Tamanho**
Define a altura e a largura da imagem.

>[!NOTE]
>
>O **Texto alternativo** no campo **Avançado** é necessária ou o componente não pode ser salvo, e a seguinte mensagem de erro é exibida:
>
>`Validation failed. Verify the values of the marked fields.`

O exemplo a seguir mostra um componente Texto e imagem (Campaign) sendo exibido.

![chlimage_1-52](assets/chlimage_1-52.png)

### Texto e personalização (Campanha) {#text-personalization-campaign}

O componente Texto e personalização (Campaign) permite que você insira um bloco de texto usando um editor WYSIWYG, com a funcionalidade fornecida pelo [Editor de Rich Text](/help/sites-authoring/rich-text-editor.md). Além disso, esse componente permite usar campos de contexto e blocos de personalização disponíveis no Adobe Campaign; consulte também [Inserir personalização](/help/sites-authoring/campaign.md#inserting-personalization).

A seleção de ícones permite que você formate o texto, incluindo características da fonte, alinhamento, links, listas e recuo. A funcionalidade é basicamente a mesma no [ambas as interfaces](/help/sites-authoring/editing-content.md), embora a aparência seja diferente:

![chlimage_1-53](assets/chlimage_1-53.png)

No editor local, é possível adicionar texto, alterar a justificação, adicionar e remover links, adicionar campos de contexto ou blocos de personalização e entrar no modo de tela cheia. Quando terminar de adicionar texto/personalização, selecione a marca de seleção para salvar suas alterações (ou x para cancelar). Consulte [Edição no local](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui) para obter mais informações.

>[!NOTE]
>
>* Os campos de personalização disponíveis dependem do modelo do Adobe Campaign ao qual o seu boletim informativo está vinculado.
>* Após selecionar uma persona no ContextHub, os campos de personalização são substituídos automaticamente pelos dados do perfil selecionado.
>
>Consulte [Inserir personalização](/help/sites-authoring/campaign.md#inserting-personalization).

![chlimage_1-54](assets/chlimage_1-54.png)

>[!NOTE]
>
>Somente os campos definidos na variável **nms:seedMember** ou uma de suas extensões é levada em conta. Os atributos das tabelas vinculadas a **nms:seedMember** não estão disponíveis.

## Componentes de formulário do Adobe Campaign {#adobe-campaign-form-components}

Use os componentes do Adobe Campaign para criar um formulário que os usuários preenchem para assinar um informativo, cancelar a assinatura de um informativo ou atualizar seus perfis de usuário. Consulte [Criação do Adobe Campaign Forms](/help/sites-authoring/adobe-campaign-forms.md) para obter mais informações.

Cada campo de componente pode ser vinculado a um campo de banco de dados do Adobe Campaign. Os campos disponíveis diferem de acordo com o tipo de dados que eles contêm, conforme descrito na seção [Componentes e tipo de dados](#components-and-data-type). Se você estender o esquema do recipient no Adobe Campaign, os novos campos estarão disponíveis nos componentes cujos tipos de dados correspondem.

Ao abrir um formulário configurado para integração com o Adobe Campaign, você verá os seguintes componentes na **Adobe Campaign** seção:

* Caixa de seleção (Campanha)
* Campo de data (Campaign) e Campo de data/HTML5 (Campaign)
* Chave primária criptografada (Campanha)
* Exibição de erro (Campaign)
* Chave de reconciliação oculta (Campanha)
* Campo numérico (Campanha)
* Campo de opções (Campanha)
* Lista de verificação de assinaturas (Campanha)
* Campo de texto (Campanha)

Os componentes são exibidos da seguinte maneira:

![chlimage_1-55](assets/chlimage_1-55.png)

Esta seção descreve cada componente em detalhes.

### Componentes e tipo de dados {#components-and-data-type}

A tabela a seguir descreve os componentes disponíveis para exibir e modificar os dados de perfil do Adobe Campaign. Cada componente pode ser mapeado para um campo de perfil do Adobe Campaign para exibir seu valor e atualizar o campo quando o formulário for enviado. Os diferentes componentes só podem ser correspondidos aos campos de um tipo de dados apropriado.

<table>
 <tbody>
  <tr>
   <td><p><strong>Componente</strong></p> </td>
   <td><p><strong>Tipo de dados do campo Adobe Campaign</strong></p> </td>
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

Na maioria dos componentes, você pode configurar o seguinte:

#### Título e texto {#title-and-text}

![chlimage_1-56](assets/chlimage_1-56.png)

* **Título**
Se quiser usar um nome diferente do nome do elemento, insira-o aqui.

* **Ocultar Título**
Marque essa caixa de seleção se não quiser que o título fique visível.

* **Descrição**
Adicione uma descrição ao campo para fornecer mais informações para os usuários.

* **Mostrar apenas valor**
Mostra apenas o valor, se houver um

#### Adobe Campaign {#adobe-campaign}

Você pode configurar o seguinte:

* **Mapeamento**
Selecione um campo de personalização do Adobe Campaign, se apropriado.

* **Chave de Reconciliação**
Marque essa caixa de seleção se esse campo fizer parte da chave de reconciliação.

![chlimage_1-57](assets/chlimage_1-57.png)

#### Restrições {#constraints}

* **Obrigatório** Marque essa caixa de seleção para tornar esse componente obrigatório; ou seja, os usuários devem inserir um valor.
* **Mensagem necessária** Opcionalmente, adicione uma mensagem informando que o campo é obrigatório.

![chlimage_1-58](assets/chlimage_1-58.png)

#### Estilo {#styling}

* **CSS**
Insira as classes CSS que deseja usar para esse componente.

![chlimage_1-59](assets/chlimage_1-59.png)

### Caixa de seleção (Campanha) {#checkbox-campaign}

O componente Caixa de seleção (Campaign) permite que o usuário modifique campos de perfil do Adobe Campaign que sejam do tipo de dados booleano. Por exemplo, você pode ter um componente Caixa de seleção (Campaign) que permite que o recipient especifique que não deseja ser contatado por meio de nenhum canal.

Você pode [definir configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components) no componente Caixa de seleção (Campaign) .

O exemplo a seguir mostra um componente Caixa de seleção (Campaign) sendo exibido.

![chlimage_1-60](assets/chlimage_1-60.png)

### Campo de data (Campaign) e Campo de data/HTML 5 (Campaign) {#date-field-campaign-and-date-field-html-campaign}

Use o campo de data para permitir que os recipients tenham uma data; por exemplo, talvez você queira que os recipients especifiquem suas datas de nascimento. O formato de data corresponde ao formato usado em sua instância do Adobe Campaign.

Além de [configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components), você pode configurar o seguinte:

* **Restrições - Restrição** menu suspenso Você pode selecionar - **Nenhum** ou **Data -** para adicionar a restrição de uma data ou nenhuma restrição. Se você selecionar data, a resposta que os usuários inserirem no campo deverá estar em um formato de data.

* **Mensagem de restrição** Além disso, é possível adicionar uma mensagem de restrição para que os usuários saibam formatar corretamente suas respostas.
* **Estilo - Largura** Ajuste a largura do campo clicando ou tocando no botão **+** e **-** ou inserir um número.

O exemplo a seguir mostra um componente Campo de data (Campaign) com a largura ajustada sendo exibida.

![chlimage_1-61](assets/chlimage_1-61.png)

### Chave primária criptografada (Campanha) {#encrypted-primary-key-campaign}

Esse componente define o nome do parâmetro de URL que conterá o identificador de um perfil do Adobe Campaign (**Identificador de recurso principal** ou **Chave primária criptografada** no Adobe Campaign Standard e 6.1, respectivamente).

Cada formulário exibindo e modificando os dados de perfil do Adobe Campaign **must** inclua um componente Chave primária criptografada.

Você pode configurar o seguinte no componente Chave primária criptografada (Campaign):

* **Título e texto - Nome do elemento** O padrão é encryptedPK. Você só precisa alterar o nome do elemento quando ele estiver em conflito com o nome de outro elemento no formulário. Dois campos de formulário não podem ter o mesmo nome de elemento.
* **Adobe Campaign - Parâmetro de URL** Adicione o parâmetro de URL para a EPK. Por exemplo, você pode usar o valor **epk**.

O exemplo a seguir mostra um componente Chave primária criptografada (Campaign) sendo exibido.

![chlimage_1-62](assets/chlimage_1-62.png)

### Exibição de erro (Campaign) {#error-display-campaign}

Esse componente permite exibir erros de backend. O tratamento de erros do formulário precisa ser definido como Encaminhar para que o componente funcione corretamente.

O exemplo a seguir mostra um componente Exibição de erro (Campaign) sendo exibido.

![chlimage_1-63](assets/chlimage_1-63.png)

### Chave de reconciliação oculta (Campanha) {#hidden-reconciliation-key-campaign}

O componente Chave de reconciliação oculta (Campaign) permite adicionar campos ocultos como parte da chave de reconciliação a um formulário.

Você pode configurar o seguinte no componente Chave de reconciliação oculta (Campaign):

* **Título e texto - Nome do elemento** O padrão é reconcilKey. Você só precisa alterar o nome do elemento quando ele estiver em conflito com o nome de outro elemento no formulário. Dois campos de formulário não podem ter o mesmo nome de elemento.
* **Adobe Campaign - Mapeamento** Mapear para um campo de personalização do Adobe Campaign.

O exemplo a seguir mostra um componente Chave de reconciliação oculta (Campaign) sendo exibido.

![chlimage_1-64](assets/chlimage_1-64.png)

### Campo numérico (Campanha) {#numeric-field-campaign}

Use o campo numérico para permitir que os recipients insiram números, por exemplo, sua idade.

Além de [configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components), você pode configurar o seguinte:

* **Restrições - Restrição** menu suspenso Você pode selecionar - **Nenhum** ou **Numérico -** para adicionar a restrição de um número ou nenhuma restrição. Se você selecionar um número, a resposta que os usuários inserirem no campo deverá ser numérica.

* **Mensagem de restrição** Além disso, é possível adicionar uma mensagem de restrição para que os usuários saibam formatar corretamente suas respostas.
* **Estilo - Largura** Ajuste a largura do campo clicando ou tocando no botão **+** e **-** ou inserir um número.

O exemplo a seguir mostra um componente Campo numérico (Campaign) com a largura configurada sendo exibida.

![chlimage_1-65](assets/chlimage_1-65.png)

### Campo de opções (Campanha) {#option-field-campaign}

Essa lista suspensa permite selecionar uma opção; por exemplo, o gênero ou status de um recipient.

Você pode [definir configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components) no componente Campo de opções (Campaign). Para preencher a lista suspensa, selecione o campo apropriado nos campos de personalização do Adobe Campaign clicando ou tocando no símbolo do Adobe Campaign e navegando até o campo .

![chlimage_1-66](assets/chlimage_1-66.png)

O exemplo a seguir mostra um componente Campo de opção (Campaign) sendo exibido.

![chlimage_1-67](assets/chlimage_1-67.png)

### Lista de verificação de assinaturas (Campanha) {#subscriptions-checklist-campaign}

Use o **Lista de verificação de assinaturas (Campaign)** para modificar as assinaturas associadas a um perfil do Adobe Campaign.

Quando adicionado a um formulário, esse componente exibe todas as assinaturas disponíveis como caixas de seleção e permite que o usuário selecione as assinaturas desejadas. Quando os usuários enviam o formulário, esse componente inscreve o usuário ou cancela a assinatura dos serviços selecionados, dependendo do tipo de ação de formulário (**Adobe Campaign: Inscrever-se nos Serviços** ou **Adobe Campaign: Cancelar assinatura dos serviços**).

>[!NOTE]
>
>O componente não verifica de quais serviços o usuário já está inscrito/cancelado.

Você pode [definir configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components) no componente Lista de verificação de assinaturas (Campaign) . (Não há configurações do Adobe Campaign disponíveis para esse componente.)

O exemplo a seguir mostra um componente Lista de verificação de assinaturas (Campaign) sendo exibido.

![chlimage_1-68](assets/chlimage_1-68.png)

### Campo de texto (Campanha) {#text-field-campaign}

O componente Campo de texto (Campaign) que permite inserir dados do tipo string, como nome, sobrenome, endereço, endereço de email e assim por diante.

Além de [configurações comuns à maioria dos componentes do Adobe Campaign](#settings-common-to-most-components), você pode configurar o seguinte:

* **Restrições - Restrição** menu suspenso Você pode selecionar - **Nenhum,** **Email** ou **Nome** (sem tremas) - para adicionar a restrição de um endereço de email, nome ou nenhuma restrição. Se você selecionar um email, a resposta que os usuários inserirem no campo deverá ser um endereço de email. Se você selecionar um nome, ele deve ser um nome (trema não são permitidos).

* **Mensagem de restrição** Além disso, é possível adicionar uma mensagem de restrição para que os usuários saibam formatar corretamente suas respostas.
* **Estilo - Largura** Ajuste a largura do campo clicando ou tocando no botão **+** e **-** ou inserir um número.

O exemplo a seguir mostra um componente Campo de texto (Campaign) sendo exibido.

![chlimage_1-69](assets/chlimage_1-69.png)
